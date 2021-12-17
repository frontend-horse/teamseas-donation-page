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
    <!-- <img src="/logo.svg" class="background" alt="" /> -->
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
  padding: 0.5rem 0;
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
}
</style>
