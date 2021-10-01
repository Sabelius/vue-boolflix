<template>
  <div>
   <input type="text" placeholder="movies" v-model="searchQuery" @keydown.enter="$emit('search', searchQuery)">
   <span class="p-2">
   <button type="button" class="btn btn-primary" @click="$emit('search', searchQuery)">Search</button>
   </span>
  </div>
</template>

<script>
export default {
    name: "Header",

    data() {
    return {
      searchQuery: " ",
    };
  },

}
</script>

<style>

</style>