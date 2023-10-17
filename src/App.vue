<template>
  <Navbar @search-music="searchMusic" />
  <div class="grid md:grid-cols-3">
    <div v-if="playlist.length > 0" class="max-h-screen overflow-y-scroll">
      <ListMusic
        :playlist="playlist"
        :selectedMusic="selectedMusic"
        @play-music="playMusic"
      />
    </div>
    <div class="hidden md:block md:md:col-span-2">
      <!-- Display selected music's preview -->
      <div
        v-if="selectedMusic.trackName != '' && !isMobile"
        class="card bg-base-100 md:min-h-[calc(100vh-64px)]"
      >
        <PlayMusic :selected-music="selectedMusic" />
      </div>
    </div>
  </div>

  <dialog id="my_modal_1" class="modal">
    <div class="modal-box">
      <PlayMusic :selected-music="selectedMusic" v-if="isMobile" />
      <div class="modal-action">
        <form method="dialog">
          <!-- if there is a button in form, it will close the modal -->
          <button class="btn">Close</button>
        </form>
      </div>
    </div>
  </dialog>
</template>

<script setup lang="ts">
import { defineComponent, ref, computed } from "vue";
import Navbar from "./components/Navbar.vue";
import ListMusic from "./components/ListMusic.vue";
import MusicDataService from "./services/MusicDataService";
import Music from "./types/Music";
import PlayMusic from "./components/PlayMusic.vue";

const selectedMusic = ref<Music>({
  trackName: "",
  artistName: "",
  artworkUrl100: "",
  primaryGenreName: "",
  releaseDate: new Date(),
});
const playlist = ref<Music[]>([]);

const searchMusic = async (searchMusic: string) => {
  try {
    const response = await MusicDataService.getAll({
      searchTerm: searchMusic,
    });
    playlist.value = response;
  } catch (error) {
    console.error("Error fetching music tracks:", error);
  }
};

const playMusic = (music: Music) => {
  // Set the selected music to the clicked music item
  selectedMusic.value = music;
};

const isMobile = computed(() => {
  return screen.width <= 760;
});
</script>

<script lang="ts">
export default defineComponent({
  name: "MyComponent",
  components: {
    Navbar,
    // Add other components used in your template
  },
});
</script>
