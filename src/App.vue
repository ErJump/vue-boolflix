<template>
  <div id="app">
    <HeaderMain @search="setQuery"/>
    <ContentMain :moviesArray="moviesList" :seriesArray="seriesList"/>
  </div>
</template>

<script>
import ContentMain from './components/ContentMain.vue'
import HeaderMain from './components/HeaderMain.vue'
import axios from 'axios';
export default {
  name: 'App',
  components: {
    ContentMain,
    HeaderMain
  },
  data: function () {
    return {
      apiKey: 'a5d177e96f7332485dbdb94d539665db',
      apiUrlMovies: 'https://api.themoviedb.org/3/search/movie',
      apiUrlSeries: 'https://api.themoviedb.org/3/search/tv',
      query: '',
      moviesList: [],
      seriesList: [],
    }
  },
  methods:{
    //chiamata per i film in base alla query
    getMovies: function (){
      axios.get(`${this.apiUrlMovies}?api_key=${this.apiKey}&query=${this.query}`)
      .then(response => {
        this.moviesList = response.data.results;
      })
      .catch(error => {
        console.log(error);
      })
    },
    //chiamata per le serie tv in base alla query
    getTvSeries: function (){
      axios.get(`${this.apiUrlSeries}?api_key=${this.apiKey}&query=${this.query}`)
      .then(response => {
        this.seriesList = response.data.results;
      })
      .catch(error => {
        console.log(error);
      })
    },
    //setta la query e invoca le chiamate per i film e le serie tv
    setQuery: function (query){
      this.query = query;
      this.getMovies();
      this.getTvSeries();
    }
  },
}
</script>

<style lang="scss">
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css");
@import "~bootstrap/dist/css/bootstrap.css";
@import "~flag-icons/css/flag-icons.css";

  #app{
    position: relative;
  }
</style>
