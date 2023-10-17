<template>
  <div class="card-body items-center justify-center text-center">
    <figure>
      <img :src="selectedMusic.artworkUrl100" alt="Song" />
    </figure>
    <h2 class="card-title">{{ selectedMusic.trackName }}</h2>
    <p>{{ selectedMusic.artistName }}</p>
    <audio :src="selectedMusic.previewUrl" controls autoplay></audio>
  </div>
</template>
<script lang="ts">
import Music from "../types/Music";
import { defineComponent } from "vue";
import type { PropType } from "vue";

export default defineComponent({
  name: "PlayMusic",
  props: {
    selectedMusic: {
      type: Object as PropType<Music>,
      required: true,
    },
  },
});
</script>
