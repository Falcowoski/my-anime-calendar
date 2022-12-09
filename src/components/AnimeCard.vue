<template>
  <q-card flat class="anime-card">
    <q-img :src="picture" width="175px" height="257.76px">
      <span class="anime-card__tag">
        <p>{{ broadcastDayOfWeek }}</p>
      </span>

      <span class="anime-card__legend">
        <p>{{ title }}</p>
      </span>
    </q-img>

    <q-card-actions class="anime-card__footer">
      <q-btn
        @click="handleClick"
        :color="added ? 'dark' : 'secondary'"
        :label="added ? 'Remover' : 'Adicionar'"
        class="full-width"
        unelevated
      />
    </q-card-actions>
  </q-card>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'AnimeCard',
  props: {
    id: {
      type: Number,
      required: true,
    },

    title: {
      type: String,
      required: true,
    },

    broadcast: {
      type: Object,
      default: null,
    },

    picture: {
      type: String,
      required: true,
    },

    added: {
      type: Boolean,
      default: false,
    },

    handleClick: {
      type: Function,
      required: true,
    },
  },

  computed: {
    broadcastDayOfWeek() {
      const days = {
        other: 'Outro',
        monday: 'Segunda',
        tuesday: 'Terça',
        wednesday: 'Quarta',
        thursday: 'Quinta',
        friday: 'Sexta',
        saturday: 'Sábado',
        sunday: 'Domingo',
      };

      // Default value!
      if (!this.broadcast) {
        return days.other;
      }

      return days[this.broadcast.day_of_the_week];
    },
  },
});
</script>

<style lang="scss">
.anime-card {
  width: 175px;
  height: auto;
}

.anime-card__tag {
  width: 80px;
  height: 32px;
  background: $info;
  position: absolute;
  top: 0;
  right: 0;
  padding: 4px 10px;

  p {
    text-align: center;
    margin: 0;
    font-weight: 600;
    font-size: 14px;
    line-height: 24px;
    color: #ffffff;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
}

.anime-card__legend {
  width: 175px;
  height: 32px;
  background: rgba(0, 0, 0, 0.6);
  position: absolute;
  bottom: 0;
  padding: 4px 10px;

  p {
    margin: 0;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    color: #ffffff;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
}

.anime-card__footer {
  padding: 0;
}
</style>
