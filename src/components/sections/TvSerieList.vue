<template>
  <div class="col-12">
    <div class="d-flex justify-content-between mb-3">
      <h2 class="text-white">TV Series</h2>
      <div class="d-flex align-items-center">
        <label class="text-white me-3 fs-4">Genres filter:</label>
        <select class="px-3 py-2 ms_select" v-model="selected">
          <option value="">All</option>
          <option v-for="genre in genres" :key="genre.id" :value="genre.id">{{genre.name}}</option>
        </select>
      </div>
    </div>
    <div class="row">
      <div class="col-12 fs-4 ms_color_grey" v-if="seriesArrayFiltered == 0">No result</div>
      <TvSerieCard v-for="serie in seriesArrayFiltered" :key="serie.id" :serie="serie" :genres="genres"/>
    </div>
  </div>
</template>

<script>
import TvSerieCard from '../commons/TvSerieCard.vue';
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
      apiGenresUrl: 'https://api.themoviedb.org/3/genre/tv/list',
      apiLanguage: 'en-US',
      genres: [],
      selected: '',
    };
  },
  methods: {
    //prende i generi delle serie tv dalla api
    getTvSeriesGenres: function (){
      axios.get(this.apiGenresUrl, {
        params: {
          api_key: this.apiKey,
          language: this.apiLanguage
        }
      })
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
  computed: {
    //restituisce solo le serie tv che hanno il genere selezionato
    seriesArrayFiltered: function (){
      if(this.selected == ''){
        return this.seriesArray;
      }
      return this.seriesArray.filter(serie => serie.genre_ids.includes(this.selected));
    }
  }
}
</script>

<style lang="scss">
  @import "../../assets/styles/variables.scss";

  .ms_select{
    background-color: $bgMain;
    color: white;
  }
  .ms_color_grey{
    color: $subtitleColor;
  }
</style>
