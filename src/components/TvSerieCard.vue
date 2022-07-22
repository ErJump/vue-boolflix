<template>
  <div class="col-3">
    <div class="ms_card py-2 position-relative">
      <img class="w-100" v-if="serie.poster_path == null || serie.poster == ''" src="http://www.movienewz.com/img/films/poster-holder.jpg" :alt="serie.name">
      <img v-else class="w-100" :src="`${apiImgUrl}${serie.poster_path}`" :alt="serie.name">
      <div class="ms_backcard">
        <img class="ms_img_back " v-if="serie.poster_path == null" src="http://www.movienewz.com/img/films/poster-holder.jpg" :alt="serie.name">
        <img v-else class="ms_img_back" :src="`${apiImgUrl}${serie.poster_path}`" :alt="serie.name">
        <ul class="w-75">
          <li>Title: {{serie.name}}</li>
          <li>Original Title: {{serie.original_name}}</li>
          <li>Original Language: <span :class="`fi fi-${changeFlag(serie.original_language)}`"></span></li>
          <li>Vote Average: 
            <i v-for="vote in getVoteAverage(serie.vote_average)" :key="vote" class="fa-solid fa-star"></i>
            <span v-if="serie.vote_average == 0">-</span> 
          </li>
          <button @click="getTvSeriesCast(serie.id); changeActiveInfo()" class="ms_button position-absolute d-flex align-items-center justify-content-center"><i class="text-white fa-solid fa-angle-right"></i></button>
        </ul>
        <div @mouseleave="setActiveInfoFalse()" v-if="activeInfo" class="position-absolute ms_card_info text-white d-flex justify-content-center align-items-center">
          <ul class="w-75">
            <h5>Cast:</h5>
            <li v-for="member in cast" :key="member.id">{{member.name}}</li>
          </ul>
          <ul class="w-75">
            <h5>Genres:</h5>
            <li v-for="(genre, index) in serie.genre_ids" :key="index">{{mapGenres(genre)}}</li>
          </ul>
          <button @click="changeActiveInfo()" class="d-flex justify-content-center align-items-center ms_button position-absolute"><i class="text-white fa-solid fa-angle-left"></i></button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'TvSerieCard',
  props:{
    serie: {
      type: Object,
      required: true
    },
    genres: {
      type: Array,
      required: true
    },
  },
  data: function () {
    return {
      apiImgUrl: "https://image.tmdb.org/t/p/w342",
      apiKey: 'a5d177e96f7332485dbdb94d539665db',
      apiUrl: 'https://api.themoviedb.org/3/tv/',
      cast: [],
      activeInfo: false,
    }
  },
  methods: {
    //cambia le iso code della lingua in una bandiera
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
    //restituisce i valori del voto medio, arrotondati, per una scala da 0 a 5
    getVoteAverage: function (vote){
      return Math.round(vote / 2);
    },
    //chiamata all'api per ottenere il cast di una serie tv, tenendo solo i primi 5 membri
    getTvSeriesCast: function (id){
      axios.get(`${this.apiUrl}${id}/credits?api_key=${this.apiKey}`)
      .then(response => {
        this.cast = response.data.cast;
        this.cast.splice(5);
      })
      .catch(error => {
        console.log(error);
      });
    },
    //cambia lo stato di activeInfo a true o false
    changeActiveInfo: function (){
      this.activeInfo = !this.activeInfo;
    },
    //cambia lo stato di activeInfo a false
    setActiveInfoFalse: function (){
      this.activeInfo = false;
    },
    //restituisce il nome del genere in base all'id del genere
    mapGenres: function (id){
      return this.genres.find(genre => genre.id == id).name;
    }
  },
}
</script>

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
    height: 50%;
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
