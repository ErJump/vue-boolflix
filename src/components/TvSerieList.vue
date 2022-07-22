<template>
  <div class="col-12">
    <h2 class="text-white">TV Series</h2>
    <div class="row">
      <TvSerieCard v-for="serie in seriesArray" :key="serie.id" :serie="serie" :genres="genres"/>
    </div>
  </div>
</template>

<script>
import TvSerieCard from './TvSerieCard.vue';
import axios from 'axios';

export default {
  name: 'TvSerieList',
  props:{
    seriesArray: {
      type: Array,
      required: true
    }
  },
  components: {
    TvSerieCard
  },
  data: function () {
    return {
      apiKey: 'a5d177e96f7332485dbdb94d539665db',
      apiGenresUrl: 'https://api.themoviedb.org/3/genre/tv/list?api_key=',
      apiLanguage: '&language=en-US',
      genres: [],
    };
  },
  methods: {
    //prende i generi delle serie tv dalla api
    getTvSeriesGenres: function (){
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
    this.getTvSeriesGenres();
  },
}
</script>

<style scoped lang="scss">
</style>
