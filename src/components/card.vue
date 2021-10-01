<template>
  <section>
    <div v-for="film in films" :key="film.id" class="pt-3">
      <img class="poster" :src="posterFunction(film)" />
      <div class="title pt-2">
        Titolo: <span class="description">{{ film.title }}</span>
      </div>
      <div class="original-title">
        Original Title:
        <span class="description">{{ film.original_title }}</span>
      </div>
      <div class="language">
        Language: <span class="description">{{ film.original_language }}</span>
      </div>
      <div class="vote">
        Voto: <span class="description" >{{ film.vote_average }}</span>
      </div>
    </div>

    <div v-for="show in series" :key="show.id" class="pt-3">
        <img class="poster" :src="posterFunction(show)" />
      <div class="title pt-2">
        Titolo: <span class="description">{{ show.name }}</span>
      </div>
      <div class="original-title">
        Original Title:
        <span class="description">{{ show.original_name }}</span>
      </div>
      <div class="language">
        Language: <span class="description">{{ show.original_language }}</span>
      </div>
      <div class="vote">
        Voto: <span class="description">{{ show.vote_average }}</span>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "card",
  props: ["films", "series"],

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

img{
    width: 300px;
}

</style>