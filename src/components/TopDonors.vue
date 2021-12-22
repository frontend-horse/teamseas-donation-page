<script>
import { toRefs } from 'vue';

export default {
  name: 'DonationCard',
  props: {
    donors: { type: Array, required: true },

    numbered: { type: Boolean, required: false, default: true }
  },
  setup(props) {
    const { numbered, donors = [] } = toRefs(props);
  }
};
</script>

<template>
  <div class="card">
    <img
      class="background"
      src="/logo.svg"
      alt="Frontend Horse: Holiday Snowtacular logo"
    />
    <component :is="numbered ? 'ol' : 'ul'">
      <li v-for="donor in donors" :key="donor.display_name">
        <span class="name">{{ donor.display_name }}</span> - ${{
          donor.donation
        }}
      </li>
    </component>
  </div>
</template>

<style scoped>
.card {
  --shadow-color: var(--color-shadow);
  background-color: var(--color-bg-secondary);
  border-radius: 10px;
  padding: 2rem 1.5rem;
  position: relative;
  overflow: hidden;
  color: var(--color-secondary);
  display: flex;
  justify-content: center;
  width: fit-content;
  margin: auto;
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
  margin: 0;
}

li {
  font-size: 1.5rem;
}

li + li {
  margin-top: 10px;
}
</style>
