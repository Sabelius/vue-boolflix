<template>
  <section>
    <div v-for="film in films" :key="film.id" class="pt-3">
      <img class="poster" :src="posterFunction(film)" />
      <div class="title pt-2">
        <strong>Titolo: </strong>
        <span class="description">{{ film.title }}</span>
      </div>
      <div class="original-title">
        <strong>Original Title: </strong>

        <span class="description">{{ film.original_title }}</span>
      </div>
      <div class="language">
        <span class="description" v-if="flags.includes(film.original_language)">
        <strong>Language: </strong><img  :src="require('../img/' + film.original_language + '.png')" class="flag"/></span>
        <span v-else><strong>Language: </strong>{{ film.original_language}}</span>
      </div>
      <div class="vote">
        <strong>Voto: </strong>
        <span class="description">{{ film.vote_average }}</span>
      </div>
    </div>

    <div v-for="show in series" :key="show.id" class="pt-3">
      <img class="poster" :src="posterFunction(show)" />
      <div class="title pt-2">
        <strong>Titolo: </strong>
        <span class="description">{{ show.name }}</span>
      </div>
      <div class="original-title">
        <strong>Original Title: </strong>

        <span class="description">{{ show.original_name }}</span>
      </div>
      <div class="language">
        <span class="description" v-if="flags.includes(show.original_language)">
        <strong>Language: </strong><img  :src="require('../img/' + show.original_language + '.png')" class="flag"/></span>
        <span v-else><strong>Language: </strong>{{ show.original_language}}</span>
      </div>
      <div class="vote">
        <strong>Voto: </strong>
        <span class="description">{{ show.vote_average }}</span>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "card",
  props: ["films", "series"],

  data() {
    return {
      flags: ["it", "en", "es", "fr", "de", "ja", "ko"],
    };
  },

  methods: {
    posterFunction(element) {
      if (element.poster_path != null) {
        return (
          "https://image.tmdb.org/t/p/w600_and_h900_bestv2" +
          element.poster_path
        );
      }
    },
  },
};
</script>

<style lang="scss" scoped>
img {
  width: 300px;
}
.flag {
  width: 30px;
}
</style>