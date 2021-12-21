<script lang="ts">
export default {
  name: 'DonationsList'
};
</script>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

import LoadingSpinner from './LoadingSpinner.vue';
import DonationCard from './DonationCard.vue';
import TopDonors from './TopDonors.vue';

import { supabase } from '@/supabase';
import { Donation } from '@/interfaces/Donation';
import { TopDonor } from '@/interfaces/TopDonor';

const isLoading = ref(true);
const errorOccurred = ref(false);

const topDonors = ref<TopDonor[] | null>(null);
const allDonations = ref<Donation[] | null>(null);
let totalDonationAmount = ref<number>(0);
const sponsorDonationIDs = [8748308, 8749386, 8751610];
let sponsorDonations = ref<Donation[] | null>(null);

onMounted(async () => {
  try {
    const { data, error } = await supabase.from<Donation>('team_seas').select();

    if (error) {
      throw error;
    }

    allDonations.value =
      data?.sort((a, b) => b.created_at - a.created_at) || null;

    const reducer = (previousValue, currentValue) =>
      previousValue + currentValue.donation;
    totalDonationAmount.value = data.reduce(reducer, 0);

    topDonors.value =
      data
        ?.reduce((donorsArr: TopDonor[], { display_name, donation, id }) => {
          const currentNameEntryIndex = donorsArr.findIndex(
            (donor) => donor.display_name === display_name
          );

          if (currentNameEntryIndex !== -1) {
            donorsArr[currentNameEntryIndex].donation += donation;
          } else {
            donorsArr.push({ display_name, donation, id });
          }

          return donorsArr;
        }, [])
        .filter((item) => {
          return !sponsorDonationIDs.includes(item.id);
        })
        .sort((a, b) => b.donation - a.donation)
        .slice(0, 10) || null;
    sponsorDonations.value = sponsorDonationIDs.map((id) =>
      data.find((item) => item.id === id)
    );
    console.log(
      '🚀 ~ file: DonationsList.vue ~ line 65 ~ onMounted ~ sponsorDonations',
      sponsorDonations
    );
  } catch (error) {
    errorOccurred.value = true;
  } finally {
    isLoading.value = false;
  }
});
</script>

<template>
  <LoadingSpinner v-if="isLoading" />
  <p v-else-if="errorOccurred" id="error-message">
    Something went wrong! Please try again later...
  </p>
  <div v-else>
    <section class="">
      <div>
        <h2>Donation Leaderboard</h2>
        <TopDonors :donors="topDonors" />
      </div>
    </section>
    <section class="">
      <div>
        <h2>Sponsor Donations</h2>
        <TopDonors :donors="sponsorDonations" />
      </div>
    </section>
    <section>
      <h2>Total Amount Donated</h2>
      <p class="donation-total">${{ totalDonationAmount }}</p>
    </section>
    <section class="all-donations">
      <h2 class="heading">All Donations</h2>
      <div class="grid">
        <DonationCard
          v-for="donation in allDonations"
          :key="donation.id"
          :donation="donation"
        />
      </div>
    </section>
  </div>
</template>

<style scoped>
#error-message {
  text-align: center;
}

.donation-total {
  font-size: 3rem;
  font-weight: bold;
  text-align: center;
}
</style>
