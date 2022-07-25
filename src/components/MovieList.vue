<template>
  <div class="col-12">
    <div class="d-flex justify-content-between mb-3">
      <h2 class="text-white">Movies</h2>
      <div class="d-flex align-items-center">
        <label class="text-white me-3 fs-4">Genres filter:</label>
        <select class="px-3 py-2 ms_select" v-model="selected">
          <option value="">All</option>
          <option v-for="genre in genres" :key="genre.id" :value="genre.id">{{mapGenres(genre.id)}}</option>
        </select>
      </div>
    </div>
    <div class="row">
      <div class="col-12 fs-4 ms_color_grey" v-if="moviesArrayFiltered == 0">No result</div>
      <MovieCard v-for="movie in moviesArrayFiltered" :key="movie.id" :movie="movie" :genres="genres"/>
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
        selected: "",
    };
  },
  methods: {
    //prende i generi dei film dalla api
    getMoviesGenres: function (){
      axios.get(`${this.apiGenresUrl}${this.apiKey}${this.apiLanguage}`)
      .then(response => {
        this.genres = response.data.genres;
      })
      .catch(error => {
        console.log(error);
      });
    },
    //restituisce il nome del genere in base all'id del genere
    mapGenres: function (id){
      return this.genres.find(genre => genre.id == id).name;
    }
  },
  created: function () {
    this.getMoviesGenres();
  },
  computed: {
    //restituisce solo le serie tv che hanno il genere selezionato
    moviesArrayFiltered: function (){
      if(this.selected == ''){
        return this.moviesArray;
      }
      return this.moviesArray.filter(serie => serie.genre_ids.includes(this.selected));
    }
  }
}
</script>

<style scoped lang="scss">
  @import "../assets/styles/variables.scss";

</style>
