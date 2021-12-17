<script lang="ts">
export default {
  name: 'DonationsList'
};
</script>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

import LoadingSpinner from './LoadingSpinner.vue';
import DonationCard from './DonationCard.vue';
import LeaderboardCard from './LeaderboardCard.vue';

import { supabase } from '@/supabase';
import { Donation } from '@/interfaces/Donation';

const isLoading = ref(true);
const errorOccurred = ref(false);
const donations = ref<Donation[] | null>(null);

onMounted(async () => {
  try {
    const { data, error } = await supabase.from<Donation>('team_seas').select();

    if (error) {
      throw error;
    }

    let sortedData = data?.sort((a, b) => {
      if (a.donation > b.donation) return -1;
      if (a.donation < b.donation) return 1;
      return 0;
    });

    donations.value = sortedData;
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
  <div v-else class="donations-grid">
    <ol class="leaderboard-list">
      <li
        v-for="(donation, index) in donations"
        :key="donation.id"
        class="leaderboard-item"
      >
        <LeaderboardCard v-if="index < 10" :donation="donation" />
      </li>
    </ol>
  </div>
</template>

<style scoped>
#error-message {
  text-align: center;
}

.donations-grid {
  --shadow-color: 208deg 16% 60%;
  background: white;
  display: grid;
  grid-template-columns: 1fr;
  grid-auto-rows: minmax(auto, auto);
  border-radius: 10px;
  padding: 1rem;
  box-shadow: 0px 0.6px 0.7px hsl(var(--shadow-color) / 0.35),
    0px 2px 2.3px -0.8px hsl(var(--shadow-color) / 0.35),
    0px 5px 5.7px -1.6px hsl(var(--shadow-color) / 0.36),
    0.1px 12.1px 13.8px -2.4px hsl(var(--shadow-color) / 0.37);
  max-width: 32rem;
  margin: 0 auto;
}

.leaderboard-list {
  padding: 0 1rem;
  margin: 0;
  font-weight: bold;
}

.leaderboard-item {
  padding: 0.5rem 0;
  flex-grow: 1;
  font-weight: 700;
  font-size: 1.2rem;
  margin: 0;
}
</style>
