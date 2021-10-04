<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-10">
        <img :src="require('../img/boolflix.png')" class="header-logo" />
      </div>
      <div class="col-lg-2 col-md-4 col-sm-5 col-6 d-flex align-items-center">
        <input
          type="text"
          placeholder="Movies and Series"
          v-model="searchQuery"
          @keydown.enter="$emit('search', searchQuery)"
        />
        <span class="p-2">
          <button
            type="button"
            class="btn btn-primary "
            @click="$emit('search', searchQuery)"
          >
            <i class="fas fa-search"></i>
          </button>
        </span>
      </div>
    </div>
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
input{
  height: 30px;
}

</style>