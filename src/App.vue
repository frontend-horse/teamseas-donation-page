<script setup lang="ts">
import DonationsList from './components/DonationsList.vue';
import DonationLeaderboard from './components/DonationLeaderboard.vue';
</script>

<template>
  <img id="logo" src="/logo.svg" />
  <h1 class="heading">A fundraiser for #TeamSeas</h1>
  <section class="description">
    <p>
      Lorem ipsum dolor, sit amet consectetur adipisicing elit. Nesciunt cumque
      maiores quia a rerum! Reprehenderit, pariatur eius. Assumenda ipsa alias
      sint doloremque voluptas deleniti, eum, minima tempore ducimus beatae
      cumque.
    </p>
  </section>
  <div class="button-group">
    <a class="button" href="https://lu.ma/fh-holiday-2021">
      Register for Event
    </a>
    <a class="button" href="https://frontend.horse/donate">
      Donate to Team Seas
    </a>
  </div>

  <h1 class="heading">Leaderboard</h1>
  <DonationLeaderboard />
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

.description {
  max-width: 48rem;
  margin: auto;
}
.button-group {
  max-width: 48rem;
  display: flex;
  gap: 1rem;
  align-items: center;
  justify-content: center;
  margin: 1rem auto;
}

.button {
  background: #334d62;
  color: white;
  text-decoration: none;
  padding: 0.75rem 1rem;
  border-radius: 1.2rem;
  transition: background 0.1s ease;
  font-weight: bold;
}

.button:hover {
  background: #41627d;
}
</style>
