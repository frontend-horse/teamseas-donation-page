<script lang="ts">
export default {
  name: 'DonationCard'
};
</script>

<script setup lang="ts">
import { Donation } from '@/interfaces/Donation';

const getDisplayMessage = (message: string) =>
  message.length > 0 ? message : 'No message available';

// eslint-disable-next-line no-undef
defineProps<{ donation: Donation }>();
</script>

<template>
  <div class="card">
    <div class="details">
      <strong class="name">{{ donation.display_name }}</strong>
      <span class="amount">${{ donation.donation }}</span>
    </div>
    <p class="message">
      {{ getDisplayMessage(donation.message_public) }}
    </p>
  </div>
</template>

<style scoped>
.card {
  background-color: white;
  border-radius: 10px;
  padding: 10px;
}

.details {
  display: flex;
}

.name {
  flex-grow: 1;
}
</style>
