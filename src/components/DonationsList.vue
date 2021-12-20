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
const latestDonations = ref<Donation[] | null>(null);

onMounted(async () => {
  try {
    const { data, error } = await supabase.from<Donation>('team_seas').select();

    if (error) {
      throw error;
    }

    latestDonations.value =
      data?.sort((a, b) => b.created_at - a.created_at) || null;

    topDonors.value =
      data
        ?.reduce((donorsArr: TopDonor[], { display_name, donation }) => {
          const currentNameEntryIndex = donorsArr.findIndex(
            (donor) => donor.display_name === display_name
          );

          if (currentNameEntryIndex !== -1) {
            donorsArr[currentNameEntryIndex].donation += donation;
          } else {
            donorsArr.push({ display_name, donation });
          }

          return donorsArr;
        }, [])
        .sort((a, b) => b.donation - a.donation)
        .slice(0, 10) || null;
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
      <h2 style="margin-top: 0" class="heading">Donation Leaderboard</h2>
      <TopDonors :donors="topDonors" />
    </section>
    <article class="all-donations">
      <h2 class="heading">All Donations</h2>
      <div class="grid">
        <DonationCard
          v-for="donation in latestDonations"
          :key="donation.id"
          :donation="donation"
        />
      </div>
    </article>
  </div>
</template>

<style scoped>
#error-message {
  text-align: center;
}
</style>
