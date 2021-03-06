<script>
export default {
  name: 'DonationsList'
};
</script>

<script setup>
import { ref, onMounted } from 'vue';

import LoadingSpinner from './LoadingSpinner.vue';
import DonationCard from './DonationCard.vue';
import TopDonors from './TopDonors.vue';

import { supabase } from '@/supabase';

const isLoading = ref(true);
const errorOccurred = ref(false);

const topDonors = ref(null);
const allDonations = ref(null);
let totalDonationAmount = ref(0);
const sponsorDonationIDs = [8748308, 8749386, 8751610, 9086562, 9315870];
let sponsorDonations = ref(null);

onMounted(async () => {
  try {
    const { data, error } = await supabase.from('team_seas').select();

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
        ?.reduce((donorsArr, { display_name, donation, id }) => {
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
        <TopDonors :donors="topDonors" :numbered="true" />
      </div>
    </section>
    <section class="">
      <div>
        <h2>Sponsor Donations</h2>
        <TopDonors :donors="sponsorDonations" :numbered="false" />
      </div>
    </section>
    <section>
      <h2>Total Amount Donated</h2>
      <p class="donation-total">
        ${{ totalDonationAmount.toLocaleString('en-US') }}
      </p>
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
