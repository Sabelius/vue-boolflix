<template>
  <div class="background">
    <div class="container">
      <div class="row pt-5">
        <!-- film -->
        <div
          v-for="film in films"
          :key="film.id"
          class="col-lg-4 col-md-6 col-12 p-3"
        >
          <div class="content-container">
            <img class="poster img-fluid" :src="posterFunction(film)" />
            <div class="content-info">
              <div class="title">
                <strong>Title: </strong>
                <span>{{ film.title }}</span>
              </div>
              <div class="original-title">
                <strong>Original Title: </strong>
                <span>{{ film.original_title }}</span>
              </div>
              <div class="language">
                <span v-if="flags.includes(film.original_language)">
                  <strong>Language: </strong
                  ><img
                    :src="require('../img/' + film.original_language + '.png')"
                    class="flag"
                /></span>
                <span v-else
                  ><strong>Language: </strong>{{ film.original_language }}</span
                >
              </div>
              <div class="vote">
                <strong>Vote: </strong>
                <span>
                  <i
                    v-for="realfilmstar in 5"
                    :key="realfilmstar"
                    :class="
                      realfilmstar < getFloatInt(film.vote_average)
                        ? 'fas fa-star'
                        : 'far fa-star'
                    "
                  ></i>
                </span>
              </div>
              <div class="overview">
                <strong>Overview: </strong>
                <span>{{ film.overview }}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- serie tv -->
        <div
          v-for="show in series"
          :key="show.id"
          class="col-lg-4 col-md-6 col-12 p-3"
        >
          <div class="content-container">
            <img class="poster img-fluid" :src="posterFunction(show)" />
            <div class="content-info">
              <div class="title">
                <strong>Titolo: </strong>
                <span>{{ show.name }}</span>
              </div>
              <div class="original-title">
                <strong>Original Title: </strong>
                <span>{{ show.original_name }}</span>
              </div>
              <div class="language">
                <span v-if="flags.includes(show.original_language)">
                  <strong>Language: </strong
                  ><img
                    :src="require('../img/' + show.original_language + '.png')"
                    class="flag"
                /></span>
                <span v-else
                  ><strong>Language: </strong>{{ show.original_language }}</span
                >
              </div>
              <div class="vote">
                <strong>Voto: </strong>
                <span>
                  <i
                    v-for="realshowstar in 5"
                    :key="realshowstar"
                    :class="
                      realshowstar < getFloatInt(show.vote_average)
                        ? 'fas fa-star'
                        : 'far fa-star'
                    "
                  ></i>
                </span>
              </div>
              <div class="overview">
                <strong>Overview: </strong>
                <span class="overview">{{ show.overview }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
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
        return "https://image.tmdb.org/t/p/w342" + element.poster_path;
      }
      return require("../img/no-image.png");
    },

    // funzione per rendere il voto un intero
    getFloatInt(element) {
      return Math.ceil(element / 2);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";

.background {
  background-color: $card-bg;
  min-height: calc(100vh - 66px);
}
.poster {
  height: 512px;
  width: 100%;
}
.title,
.original-title,
.overview {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.flag {
  width: 30px;
}
.fa-star {
  color: $color-star;
}
.content-container {
  position: relative;
}
.content-info {
  transition: 0.5s ease;
  width: 80%;
  opacity: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-60%, -50%);
  color: $info-color;
}
.content-container:hover .poster {
  opacity: 0.3;
  cursor: pointer;
}
.content-container:hover .content-info {
  opacity: 1;
  cursor: pointer;
}
</style>