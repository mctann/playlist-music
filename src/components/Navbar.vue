<template>
<div class="navbar p-4 bg-base-100">
  <div class="flex-none">
    <a class="btn btn-ghost normal-case text-xl">Music</a>
  </div>
  <div class="flex-1 space-x-4">
    <div class="form-control w-full md:ml-16">
      <input v-model="searchText" type="text" placeholder="Search artist, album, title" class="input input-bordered w-full" />
    </div>
    <button class="btn btn-primary" @click="search">Search</button>
  </div>
</div>
</template>

<script lang="ts">
import { ref } from "vue";
export default {
  name: 'Navbar',
  setup(_, { emit }) {
    const searchText = ref("");
    const search = () => {

      emit('search-music', searchText.value);
    };

    return {
      searchText,
      search,
    };
  },
};
</script>