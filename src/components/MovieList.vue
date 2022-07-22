<template>
    <div class="col-12">
      <h2 class="text-white">Movies</h2>
      <div class="row">
        <MovieCard v-for="movie in moviesArray" :key="movie.id" :movie="movie" :genres="genres"/>
      </div>
    </div>
</template>

<script>
import MovieCard from './MovieCard.vue';
import axios from 'axios';

export default {
  name: "MovieList",
  components: { 
    MovieCard 
  },
  props: {
      moviesArray: {
        type: Array,
        required: true
      }
  },
  data: function () {
    return {
        apiKey: 'a5d177e96f7332485dbdb94d539665db',
        apiGenresUrl: "https://api.themoviedb.org/3/genre/movie/list?api_key=",
        apiLanguage: "&language=en-US",
        genres: [],
    };
  },
  methods: {
    getMoviesGenres: function (){
      axios.get(`${this.apiGenresUrl}${this.apiKey}${this.apiLanguage}`)
      .then(response => {
        this.genres = response.data.genres;
      })
      .catch(error => {
        console.log(error);
      });
    },
  },
  created: function () {
    this.getMoviesGenres();
  },
}
</script>

<style scoped lang="scss">
  
</style>
