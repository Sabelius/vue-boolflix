<template>
  <div>
    <div>
      <Header @search="getTitles" />
    </div>
    <div>
      <card :films="films" :series="series"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Header from "../components/Header.vue";
import card from "./card.vue";

export default {
  name: "All",
  components: {
    Header,
    card,
  },

  data() {
    return {
      films: [],
      series: [],
      myApiKey: "52cb5d6900c357a14da82ab07f3e8045",
      apiUrl: "https://api.themoviedb.org/3/search/",
      searchQuery: "",
    };
  },

  methods: {
    MoviesSearch() {
      axios
        .get(this.apiUrl + "movie", {
          params: {
            api_key: this.myApiKey,
            query: this.searchQuery,
          },
        })
        .then((element) => {
          this.films = element.data.results;
        });
    },

    SeriesSearch() {
      axios
        .get("https://api.themoviedb.org/3/search/tv", {
          params: {
            api_key: "b2f2dc9b456519ffb2d7406a9523fda2",
            query: this.searchQuery,
          },
        })
        .then((element) => {
          this.series = element.data.results;
        });
    },

    getTitles(searchQuery) {
      this.searchQuery = searchQuery;
      if (this.searchQuery != "") {
        this.MoviesSearch();
        this.SeriesSearch();
      }
    },
  },
};
</script>

<style>
</style>