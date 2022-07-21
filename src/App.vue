<template>
  <div id="app">
    <HeaderMain/>
    <ContentMain/>
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
      query: 'star',
    }
  },
  methods:{
    getMovies: function (){
      console.log(`${this.apiUrlMovies}?api_key=${this.apiKey}`)
      axios.get(`${this.apiUrlMovies}?api_key=${this.apiKey}&query=${this.query}`)
      .then(response => {
        console.log(response.data.results);
      })
      .catch(error => {
        console.log(error);
      })
    }
  },
  created(){
    this.getMovies();
  }
}
</script>

<style lang="scss">
@import "~bootstrap/dist/css/bootstrap.css";
</style>
