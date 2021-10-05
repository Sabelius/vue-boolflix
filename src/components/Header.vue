<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-2 d-flex align-items center">
        <img :src="require('../img/boolflix.png')" class="header-logo img-fluid" />
      </div>
      <div class="col-8 d-flex align-items-center justify-content-center">
        <input
          type="text"
          placeholder="Movies and Series"
          v-model="searchQuery"
          @keydown.enter="$emit('search', searchQuery)"
        />
        <span class="p-2">
          <button
            type="button"
            class="btn btn-primary"
            @click="$emit('search', searchQuery)"
          >
            <i class="fas fa-search"></i>
          </button>
        </span>
      </div>
        <div class="col-2 d-flex align-items-center">
          <select
            v-model="selectedGenre"
            @change="$emit('change', selectedGenre)"
          >
           <option value="">All</option>
            <option v-for="genre in genres" :key="genre.id" :value="genre.id">
              {{ genre.name }}
            </option>
          </select>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: ["genres"],
  data() {
    return {
      searchQuery: " ",
      selectedGenre: "",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";

div {
  background-color: $header-bg;
}
.header-logo {
  width: 200px;
}
input {
  height: 40px;
  width: 200px;
}
button{
  height: 40px;
}
</style>