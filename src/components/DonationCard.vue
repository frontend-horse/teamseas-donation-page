<script lang="ts">
export default {
  name: 'DonationCard'
};
</script>

<script setup lang="ts">
import { Donation } from '@/interfaces/Donation';

// eslint-disable-next-line no-undef
defineProps<{ donation: Donation }>();
</script>

<template>
  <div class="card">
    <img
      class="background"
      src="/logo.svg"
      alt="Frontend Horse: Holiday Snowtacular logo"
    />
    <div class="details">
      <p class="name">{{ donation?.display_name }}</p>
      <span class="amount">${{ donation?.donation }}</span>
    </div>
    <p v-if="donation?.message_public" class="message">
      {{ donation.message_public }}
    </p>
  </div>
</template>

<style scoped>
.card {
  --shadow-color: 208deg 16% 90%;
  background-color: white;
  border-radius: 10px;
  padding: 1rem;
  position: relative;
  overflow: hidden;
  box-shadow: 0px 0.6px 0.7px hsl(var(--shadow-color) / 0.35),
    0px 2px 2.3px -0.8px hsl(var(--shadow-color) / 0.35),
    0px 5px 5.7px -1.6px hsl(var(--shadow-color) / 0.36),
    0.1px 12.1px 13.8px -2.4px hsl(var(--shadow-color) / 0.37);
}
.background {
  opacity: 0.05;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: auto;
  pointer-events: none;
}

.details {
  display: flex;
}

.name {
  flex-grow: 1;
  font-weight: 700;
  font-size: 1.2rem;
  margin: 0;
  color: var(--color-secondary);
}
</style>
