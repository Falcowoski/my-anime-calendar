<template>
  <router-view />
</template>

<script>
import { defineComponent } from 'vue';
import animeSeason from './assets/data/anime_season_2022_fall.json';

export default defineComponent({
  name: 'App',

  created() {
    // Save the current anime season in the Client Local Storage
    localStorage.setItem('anime_season', JSON.stringify(animeSeason));
  },
});
</script>
