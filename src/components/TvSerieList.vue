<template>
    <div class="col-6">
        <h2>TV Series</h2>
        <ul class="py-2" v-for="serie in seriesArray" :key="serie.id">
          <img v-if="serie.poster_path == null" src="http://www.movienewz.com/img/films/poster-holder.jpg" :alt="serie.name">
          <img v-else class="w-50" :src="`${apiImgUrl}${serie.poster_path}`" :alt="serie.name">
          <li>Title: {{serie.name}}</li>
          <li>Original Title: {{serie.original_name}}</li>
          <li>Original Language: <span :class="`fi fi-${changeFlag(serie.original_language)}`"></span></li>
          <li>Vote Average: 
            <i v-for="vote in getVoteAverage(serie.vote_average)" :key="vote" class="fa-solid fa-star"></i>
            <span v-if="serie.vote_average == 0">-</span> 
          </li>
        </ul>
      </div>
</template>

<script>
export default {
  name: 'TvSerieList',
  props:{
    seriesArray: {
      type: Array,
      required: true
    }
  },
  data: function () {
    return {
      apiImgUrl: "https://image.tmdb.org/t/p/w342",
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
    getVoteAverage: function (vote){
      return Math.round(vote / 2);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
