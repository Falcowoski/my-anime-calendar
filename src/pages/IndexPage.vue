<template>
  <q-page class="container">
    <AnimeCard
      v-for="anime in animes"
      :key="anime.id"
      :id="anime.id"
      :title="anime.title"
      :broadcast="anime.broadcast"
      :picture="anime.main_picture.large"
      :added="anime.added"
      :handleClick="() => handleClick(anime.id)"
    />
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';
import AnimeCard from 'src/components/AnimeCard.vue';

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

  watch: {
    animes: {
      handler() {
        this.setAnimes();
      },
      deep: true,
    },
  },

  methods: {
    getAnimes() {
      this.animes = JSON.parse(localStorage.getItem('anime_season'));
    },

    setAnimes() {
      localStorage.setItem('anime_season', JSON.stringify(this.animes));
    },

    handleClick(id) {
      // Get index
      const index = this.animes.findIndex((anime) => anime.id === id);

      // Get object
      const anime = this.animes[index];

      // Invert the value
      anime.added = !anime.added;

      // Update state
      this.animes[index] = anime;
    },
  },

  components: { AnimeCard },
});
</script>

<style lang="scss">
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 175px);
  justify-content: center;
  gap: 1rem;
  padding: 18px 4px;
}

</style>
