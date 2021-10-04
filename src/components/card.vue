<template>
  <section>

    <!-- film -->
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
        <span v-else><strong>Language: </strong>{{ film.original_language }}</span>
      </div>
      <div class="vote">
        <strong>Voto: </strong>
        <span class="description">
          <i v-for="realfilmstar in getFloatInt(film.vote_average)" :key="realfilmstar" class="fas fa-star"></i>
          <i v-for="maxfilmstar in (5 - getFloatInt(film.vote_average))" :key="maxfilmstar" class="far fa-star"></i>
        </span>
      </div>
    </div>
    
    <!-- serie tv -->
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
        <span v-else><strong>Language: </strong>{{ show.original_language }}</span>
      </div>
      <div class="vote">
        <strong>Voto: </strong>
        <span class="description">
          <i v-for="realshowstar in getFloatInt(show.vote_average)" :key="realshowstar" class="fas fa-star"></i>
          <i v-for="maxshowstar in (5 - getFloatInt(show.vote_average))" :key="maxshowstar" class="far fa-star"></i>
          </span>
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

    // funzione che trova la locandina se questa esiste
    posterFunction(element) {
      if (element.poster_path != null) {
        return (
          "https://image.tmdb.org/t/p/w342" +
          element.poster_path
        );
      } return require('../img/no-image.png');
    },

    // funzione per rendere il voto un intero 
     getFloatInt(element){
       return Math.floor(element / 2);
     }
  },
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";

.flag {
  width: 30px;
}
.fa-star{
  color: $color-star;
}

</style>