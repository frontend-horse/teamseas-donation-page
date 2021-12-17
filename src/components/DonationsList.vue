<script lang="ts">
export default {
  name: 'DonationsList'
};
</script>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

import LoadingSpinner from './LoadingSpinner.vue';
import DonationCard from './DonationCard.vue';

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

    donations.value = data;
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
  <div v-else class="grid">
    <DonationCard
      v-for="donation in donations"
      :key="donation.id"
      :donation="donation"
    />
  </div>
</template>

<style scoped>
#error-message {
  text-align: center;
}
</style>
