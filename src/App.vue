<script setup lang="ts">
import DonationsList from './components/DonationsList.vue';
</script>

<template>
  <img id="logo" src="logo.svg" />
  <h1 class="heading">A fundraiser for #TeamSeas</h1>
  <p>
    Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nesciunt cumque
    maiores quia a rerum! Reprehenderit, pariatur eius. Assumenda ipsa alias
    sint doloremque voluptas deleniti, eum, minima tempore ducimus beatae
    cumque.
  </p>
  <h1 class="heading">All the lovely people who donated!</h1>
  <DonationsList />
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');

html,
body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

body {
  font-family: 'Poppins', sans-serif;
  color: #334d62;
  background-color: #ecf3f9;
  display: flex;
  justify-content: center;
}

#app {
  flex: 0.75;
}

#logo {
  display: block;
  margin: 32px auto 0 auto;
}

.heading {
  color: #d04447;
  margin-top: 48px;
  text-align: center;
}
</style>
