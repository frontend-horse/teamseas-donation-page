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
      data?.sort((a, b) => b.created_at - a.created_at).slice(0, 9) || null;

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
  <h1 class="heading">Our latest donations</h1>
  <LoadingSpinner v-if="isLoading" />
  <p v-else-if="errorOccurred" id="error-message">
    Something went wrong! Please try again later...
  </p>
  <div v-else>
    <div class="grid">
      <DonationCard
        v-for="donation in latestDonations"
        :key="donation.id"
        :donation="donation"
      />
    </div>
    <h1 style="margin-top: 0" class="heading">And our all-time top donors</h1>
    <div id="top-donors">
      <TopDonors :donors="topDonors" />
    </div>
  </div>
</template>

<style scoped>
#error-message {
  text-align: center;
}

#top-donors {
  padding-bottom: 3rem;
  display: flex;
  justify-content: center;
}
</style>
