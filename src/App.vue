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
    getMovies: function (){
      axios.get(`${this.apiUrlMovies}?api_key=${this.apiKey}&query=${this.query}`)
      .then(response => {
        this.moviesList = response.data.results;
      })
      .catch(error => {
        console.log(error);
      })
    },
    getTvSeries: function (){
      axios.get(`${this.apiUrlSeries}?api_key=${this.apiKey}&query=${this.query}`)
      .then(response => {
        this.seriesList = response.data.results;
        console.log(this.seriesList);
      })
      .catch(error => {
        console.log(error);
      })
    },
    
    setQuery: function (query){
      this.query = query;
      this.getMovies();
      this.getTvSeries();
    }
  },
}
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.css";
@import "~flag-icons/css/flag-icons.css";
</style>
