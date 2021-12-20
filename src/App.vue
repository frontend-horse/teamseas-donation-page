<script setup lang="ts">
import InlineSvg from 'vue-inline-svg';
import DonationsList from './components/DonationsList.vue';
</script>

<template>
  <h1>
    <inline-svg
      src="/logo.svg"
      fill="black"
      aria-label="Frontend Horse: Holiday Snowtacular"
    ></inline-svg>
  </h1>
  <h2>A fundraiser for #TeamSeas</h2>

  <div class="video-wrapper">
    <iframe
      width="560"
      height="315"
      src="https://www.youtube-nocookie.com/embed/_tbgg8-q5pY"
      title="Holiday Snowtacular Live Stream"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
    ></iframe>
  </div>

  <h2>12 Special Guests</h2>
  <section class="guests">
    <ul>
      <li>Dave Rupert</li>
      <li>Kevin Powell</li>
      <li>George Francis</li>
      <li>Monica Powell</li>
      <li>Michael Chan</li>
      <li>Josh Comeau</li>
      <li>Kent C. Dodds</li>
      <li>Chris Coyier</li>
      <li>Varun Vachhar</li>
      <li>Cassidy Williams</li>
      <li>Scott Hanselman</li>
      <li>Amelia Wattenberger</li>
    </ul>
  </section>
  <section class="sponsors">
    <h2>A huge thanks to our company sponsors</h2>

    <a href="https://prismic.io/">
      <img src="/sponsors/prismic.svg" alt="Prismic logo" />
    </a>
    <a href="https://www.netlify.com/">
      <img src="/sponsors/netlify.png" alt="Netlify logo" />
    </a>
    <a href="https://cloudinary.com/">
      <img src="/sponsors/cloudinary.png" alt="Cloudinary logo" />
    </a>
    <a href="https://stepzen.com/">
      <img src="/sponsors/stepzen.svg" alt="StepZen logo" />
    </a>
    <a href="https://orbit.love/">
      <img id="orbit-logo" src="/sponsors/orbit.svg" alt="Orbit logo" />
    </a>
  </section>
  <DonationsList />
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap');

html,
body {
  margin: 0 0 32px 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

body {
  font-family: 'Poppins', sans-serif;
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
  text-align: center;
}

.button:hover {
  background: #41627d;
}

.grid {
  display: grid;
  grid-template-columns: 1fr;
  grid-auto-rows: minmax(120px, auto);
  grid-column-gap: 20px;
  grid-row-gap: 20px;
  justify-items: stretch;
  align-items: stretch;
  padding-bottom: 64px;
}

@media (min-width: 992px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 576px) {
  .grid {
    grid-template-columns: 1fr;
  }

  .guests ul {
    flex-direction: column;
  }
}

.sponsors {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 3.5rem;
  background: #eee;
  border-radius: var(--border-radius);
  box-shadow: var(--box-shadow) var(--color-shadow);
}

.sponsors img {
  width: 320px;
  height: auto;
  object-fit: contain;
}

#orbit-logo {
  width: 250px;
}

.guests {
  max-width: 64rem;
  margin: 2rem auto;
}

.guests h2 {
  text-align: center;
}
.guests ul {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 1rem;
  text-align: center;
  list-style: none;
  font-size: 1.5rem;
  padding: 0;
  margin: 0;
}

.guests {
  color: var(--color-secondary);
}

.guests li:nth-child(even) {
  color: var(--color);
}

.svg-red {
  fill: var(--color);
}
.svg-blue {
  fill: var(--color-secondary);
}

.video-wrapper {
  margin: auto;
  display: flex;
  justify-content: center;
}
</style>
