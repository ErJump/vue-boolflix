<template>
    <div class="col-12">
      <h2 class="text-white">Movies</h2>
      <div class="row">
        <MovieCard v-for="movie in moviesArray" :key="movie.id" :movie="movie"/>
      </div>
    </div>
</template>

<script>
import MovieCard from './MovieCard.vue';

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
        apiImgUrl: "https://image.tmdb.org/t/p/w342",
        apiKey: "a5d177e96f7332485dbdb94d539665db",
        apiUrl: "https://api.themoviedb.org/3/movie/",
        cast: [],
        activeInfo: false,
        apiGenresUrl: "https://api.themoviedb.org/3/genre/movie/list?api_key=",
        apiLanguage: "&language=en-US",
        genres: [],
    };
  },
}
</script>

<style scoped lang="scss">
  
</style>
