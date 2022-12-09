<template>
  <router-view />
</template>

<script>
import { defineComponent } from 'vue';
import animeSeason from './assets/data/anime_season_2022_fall.json';

export default defineComponent({
  name: 'App',

  created() {
    // Skip this step if already has data in the Local Storage
    if (localStorage.getItem('anime_season') !== null) {
      console.warn('Already has data in Local Storage. Skipping loading.');
      return;
    }

    // Save the current anime season in the Client Local Storage
    console.warn('Saving data in the Local Storage.');
    const animes = Object.values(animeSeason.data).map((anime) => anime.node);
    localStorage.setItem('anime_season', JSON.stringify(animes));
  },
});
</script>
