<template>
  <q-page class="flex flex-center">
    <h2>É os guri!</h2>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'IndexPage',

  data() {
    return {
      animes: null,
    };
  },

  created() {
    this.getAnimes();
  },

  methods: {
    getAnimes() {
      this.animes = localStorage.getItem('anime_season');
    },
  },
});
</script>
