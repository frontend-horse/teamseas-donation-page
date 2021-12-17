<script lang="ts">
export default {
  name: 'DonationCard'
};
</script>

<script setup lang="ts">
import { Donation } from '@/interfaces/Donation';

const getDisplayMessage = (message: string) =>
  message.length > 0 ? message : 'No ';

// eslint-disable-next-line no-undef
defineProps<{ donation: Donation }>();
</script>

<template>
  <div class="card">
    <div class="details">
      <p class="name">{{ donation.display_name }}</p>
      <span class="amount">
        <strong>${{ donation.donation }}</strong>
      </span>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-left:0.5rem;
}

.details {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.name {
  padding: 0;
  margin: 0;
}
</style>
