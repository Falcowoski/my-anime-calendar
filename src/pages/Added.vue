<template>
  <q-page class="container" v-if="addedAnimes.length > 0">
    <AnimeCard
      v-for="anime in addedAnimes"
      :key="anime.id"
      :id="anime.id"
      :title="anime.title"
      :broadcast="anime.broadcast"
      :picture="anime.main_picture.large"
      :added="anime.added"
      :handleClick="() => handleClick(anime.id)"
    />
  </q-page>

  <q-page class="flex flex-center container-empty" v-else>
      <div class="flex justify-center">
        <q-icon name="sentiment_dissatisfied" size="10rem" color="dark" />
        <h6 class="text-center">Você ainda não tem nenhum anime adicionado à sua lista!</h6>
      </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';
import AnimeCard from 'src/components/AnimeCard.vue';

export default defineComponent({
  name: 'AddedPage',
  data() {
    return {
      animes: null,
      addedAnimes: null,
    };
  },

  created() {
    this.getAnimes();
    this.getAddedAnimes();
  },

  watch: {
    animes: {
      handler() {
        this.setAnimes();
        this.getAddedAnimes();
      },
      deep: true,
    },
  },

  methods: {
    getAnimes() {
      this.animes = JSON.parse(localStorage.getItem('anime_season'));
    },

    getAddedAnimes() {
      this.addedAnimes = JSON.parse(localStorage.getItem('anime_season')).filter((anime) => anime.added);
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
  grid-template-columns: repeat(auto-fill, 168px);
  justify-content: center;
  gap: 1rem;
  padding: 18px 14px;
}

.container-empty {
  opacity: 0.4;
}
</style>
