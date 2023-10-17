<template>
    <ul class="menu menu-sm bg-base-200">
      <li v-for="(item, index) in playlist" :key="index" class="py-2">
        <div :class="getSelectedMusicClass(item, selectedMusic)" @click="playMusic(item)">
          <figure>
            <img :src="item.artworkUrl100" alt="Album" />
          </figure>
          <div class="card-body">
            <p>
              {{ getTitleCard(item.artistName, item.releaseDate) }}
              <span :class="getChipColorClass(item.primaryGenreName)">{{
                item.primaryGenreName
              }}</span>
            </p>
            <h2 class="card-title">
              {{ item.trackName }}
            </h2>

            <div class="card-actions justify-end">
              <button class=" btn btn-primary btn-sm btn-circle hidden md:flex">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="#FFFFFF"
                  height="24"
                  viewBox="0 -960 960 960"
                  width="24"
                >
                  <path
                    d="M320-200v-560l440 280-440 280Zm80-280Zm0 134 210-134-210-134v268Z"
                  />
                </svg>
              </button>
              <button class="btn btn-primary btn-sm btn-circle md:hidden" onclick="my_modal_1.showModal()">   <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="#FFFFFF"
                  height="24"
                  viewBox="0 -960 960 960"
                  width="24"
                >
                  <path
                    d="M320-200v-560l440 280-440 280Zm80-280Zm0 134 210-134-210-134v268Z"
                  />
                </svg></button>
            </div>
          </div>
        </div>
      </li>
    </ul>
</template>

<script setup lang="ts">
const emit = defineEmits(["play-music"]);

const getChipColorClass = (genre: string) => {
  const genreClasses: Record<string, string> = {
    Pop: "badge-primary",
    Rock: "badge-neutral",
    Alternative: "badge-secondary",
    Electronica: "badge-accent",
  };

  const defaultClass = "badge";

  return defaultClass + " " + (genreClasses[genre] || "badge-primary");
};


const getSelectedMusicClass = (list: Music, selected: Music) => {
  let selectedClass = "card lg:card-side bg-base-100";
  if (list === selected) {
    selectedClass = selectedClass + " active"
  }
  return selectedClass;
};

const getTitleCard = (artist: string, releaseDate: Date) => {
  const date = new Date(releaseDate);
  return `${artist} • ${date.getFullYear()}`;
};

const playMusic = (music: Music) => {
  emit("play-music", music);
};
</script>

<script lang="ts">
import Music from "../types/Music";
import { defineComponent } from "vue";
import type { PropType } from "vue";

export default defineComponent({
  name: "ListMusic",
  props: {
    playlist: {
      type: Array as PropType<Music[]>,
      required: true,
    },
    selectedMusic: {
      type: Object as PropType<Music>,
      required: true,
    },
  },
});
</script>
