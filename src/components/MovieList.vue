<template>
    <div class="col-12">
      <h2 class="text-white">Movies</h2>
      <div class="row">
        <div class="col-3 ms_card py-2 position-relative" v-for="movie in moviesArray" :key="movie.id">
          <img class="w-100" v-if="movie.poster_path == null || movie.poster == ''" src="http://www.movienewz.com/img/films/poster-holder.jpg" :alt="movie.name">
          <img v-else class="w-100" :src="`${apiImgUrl}${movie.poster_path}`" :alt="movie.name">
          <div class="ms_backcard">
            <img class="ms_img_back " v-if="movie.poster_path == null" src="http://www.movienewz.com/img/films/poster-holder.jpg" :alt="movie.name">
            <img v-else class="ms_img_back" :src="`${apiImgUrl}${movie.poster_path}`" :alt="movie.name">
            <ul>
              <li>Title: {{movie.title}}</li>
              <li>Original Title: {{movie.original_title}}</li>
              <li>Original Language: <span :class="`fi fi-${changeFlag(movie.original_language)}`"></span></li>
              <li>Vote Average: 
                <i v-for="vote in getVoteAverage(movie.vote_average)" :key="vote" class="fa-solid fa-star"></i>
                <span v-if="movie.vote_average == 0">-</span> 
              </li>
              <button @click="getMovieCast(movie.id); changeActiveInfo()" class="ms_button position-absolute d-flex align-items-center justify-content-center"><i class="text-white fa-solid fa-angle-right"></i></button>
            </ul>
            <div @mouseleave="setActiveInfoFalse()" v-if="activeInfo" class="position-absolute ms_card_info text-white d-flex justify-content-center align-items-center">
              <ul>
                <span>Cast:</span>
                <li v-for="member in cast" :key="member.id">{{member.name}}</li>
              </ul>
              <ul>
                <span>Genres:</span>
                <li v-for="(genre, index) in movie.genre_ids" :key="index">{{mapGenres(genre)}}</li>
              </ul>
              <button @click="changeActiveInfo()" class="d-flex justify-content-center align-items-center ms_button position-absolute"><i class="text-white fa-solid fa-angle-left"></i></button>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'MovieList',
  props:{
    moviesArray: {
      type: Array,
      required: true
    }
  },
  data: function () {
    return {
      apiImgUrl: "https://image.tmdb.org/t/p/w342",
      apiKey: 'a5d177e96f7332485dbdb94d539665db',
      apiUrl: 'https://api.themoviedb.org/3/movie/',
      cast: [],
      activeInfo: false,
      apiGenresUrl: 'https://api.themoviedb.org/3/genre/movie/list?api_key=',
      apiLanguage: '&language=en-US',
      genres: [],
    }
  },
  methods: {
    changeFlag: function (lang) {
      switch (lang) {
          case "en":
              return "gb";
          case "ja":
              return "jp";
          case "ko":
              return "kr";
          case "cs":
              return "cz";
      }
      return lang;
    },
    getMovieCast: function (id){
      axios.get(`${this.apiUrl}${id}/credits?api_key=${this.apiKey}`)
      .then(response => {
        this.cast = response.data.cast;
        this.cast.splice(5);
        console.log(this.cast);
      })
      .catch(error => {
        console.log(error);
      });
    },
    getVoteAverage: function (vote){
      return Math.round(vote / 2);
    },
    changeActiveInfo: function (){
      this.activeInfo = !this.activeInfo;
    },
    setActiveInfoFalse: function (){
      this.activeInfo = false;
    },
    getMoviesGenres: function (){
      axios.get(`${this.apiGenresUrl}${this.apiKey}${this.apiLanguage}`)
      .then(response => {
        this.genres = response.data.genres;
      })
      .catch(error => {
        console.log(error);
      });
    },
    mapGenres: function (id){
      return this.genres.find(genre => genre.id == id).name;
    }
  },
  created: function () {
    this.getMoviesGenres();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .ms_backcard{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgb(0,0,0);
    display: none;
    flex-direction: column;
    justify-content: start;
    align-items: center;
    z-index: 1;
    gap: 1rem;
    *{
      color: white;
    }
    ul{
      list-style: none;
      padding: 0;
      margin: 0;
      li{
        width: 100%;
      }
    }
    i{
      color: rgb(216, 168, 45)
    }
  }
  .ms_card{
    transition: .5s;
    &:hover{
      transform: scale(1.2);
      z-index: 4;
    }
  }
  .ms_card:hover .ms_backcard{
    display: flex;
  }
  .ms_img_back{
    object-fit: cover;
    width: 100%;
    height: 70%;
  }
  .ms_button{
  padding: 10px;
  background-color: black;
  border: none;
  align-items: center!important;
  display: flex;
  border: 1px solid white;
  border-radius: 50%;
  right: 10px;
  top: 10px;
  width: 38px;
  }
  .ms_card_info{
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgb(0,0,0);
    display: none;
    flex-direction: column;
    justify-content: start;
    align-items: center;
    z-index: 2;
    gap: 1rem;
  }
  .ms_active{
    display: flex;
  }
  
</style>
