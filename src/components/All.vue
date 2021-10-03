<template>
  <div>
    <div>
      <Header @search="getTitles" />
    </div>
    <div>
      <card :films="films" :series="series" />
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

    // funzione che trova tutti i film 
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

    // funzione che trova tutte le serie tv
    SeriesSearch() {
      axios
        .get(this.apiUrl + "tv", {
          params: {
            api_key: this.myApiKey,
            query: this.searchQuery,
          },
        })
        .then((element) => {
          this.series = element.data.results;
        });
    },
    
    // funzione che permette la ricerca dei film e delle serie esistenti
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