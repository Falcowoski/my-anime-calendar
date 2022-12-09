<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          {{ $route.name }}
        </q-toolbar-title>

        <q-btn flat round icon="sync" @click="confirmSync" />

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    >
      <q-list>
        <q-item-label
          header
        >
          <span class="text-h6">
            My Anime Calendar
          </span>
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue';
import { useQuasar } from 'quasar';
import { useRouter } from 'vue-router';

import EssentialLink from 'components/EssentialLink.vue';
import animeSeason from '../assets/data/anime_season_2022_fall.json';

const linksList = [
  {
    title: 'Home',
    icon: 'home',
    link: '/',
  },
  {
    title: 'Adicionados',
    icon: 'notifications',
    link: '/added',
  },
];

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink,
  },

  setup() {
    const $q = useQuasar();
    const router = useRouter();
    const leftDrawerOpen = ref(false);

    function handleSync() {
      // Save the current anime season in the Client Local Storage
      const animes = Object.values(animeSeason.data).map((anime) => anime.node);
      localStorage.setItem('anime_season', JSON.stringify(animes));

      // Refresh page
      router.go();
    }

    function confirmSync() {
      $q.dialog({
        title: 'Você perderá todos os animes adicionados à sua lista.',
        message: 'Tem certeza que deseja continuar?',
        cancel: true,
        persistent: true,
      }).onOk(() => {
        handleSync();
      });
    }

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      confirmSync,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>

<style lang="scss">

</style>
