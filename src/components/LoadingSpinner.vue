<script lang="ts">
export default {
  name: 'DonationCard'
};
</script>

<template>
  <div class="lds-dual-ring"></div>
</template>

<style scoped>
.lds-dual-ring {
  display: block;
  width: 80px;
  height: 80px;
  margin: 0 auto;
}
.lds-dual-ring:after {
  /* prettier-ignore */
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #d04447;
  border-color: #d04447 transparent #d04447 transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
