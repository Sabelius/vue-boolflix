<template>
  <div>
    <div>
      <Header @search="getTitles" :genres="genres" @change="searchGenre"/>
    </div>
    <div>
      <card :films="getGenreMovieId" :series="getGenreSeriesId" />
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
      genres: [],
      selectedGenre: "",
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
    
    searchGenre(genre){
      this.selectedGenre = genre;
      console.log(genre)
    }
  },

  mounted() {
    // vengono richiamati i generi dei film
    axios
      .get("https://api.themoviedb.org/3/genre/movie/list", {
        params: {
          api_key: this.myApiKey,
          query: this.searchQuery,
        },
      })
      .then((element) => {
        this.genres = element.data.genres;
      });

    //  vengono richiamati i generi delle serie
      axios
      .get("https://api.themoviedb.org/3/genre/tv/list", {
        params: {
          api_key: this.myApiKey,
          query: this.searchQuery,
        },
      })
      .then((element) => {
        this.genres = element.data.genres;
      });
  },

  computed: {

    // funzione che seleziona i film in base al genere
    getGenreMovieId(){
      let newList = [];
      if (this.selectedGenre != ""){
        newList = this.films.filter(
          (element) =>{
           return element.genre_ids.includes(this.selectedGenre)
          } 
        );
      }else{
        return this.films;
      }
      return newList;
    },

    // funzione che seleziona le serie in base al genere
    getGenreSeriesId(){
      let newList = [];
      if (this.selectedGenre != ""){
        newList = this.series.filter(
          (element) =>{
           return element.genre_ids.includes(this.selectedGenre)
          } 
        );
      }else{
        return this.series;
      }
      return newList;
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../style/variables.scss";
</style>