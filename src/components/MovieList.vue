<template>
    <div class="col-6">
      <h2>Movies</h2>
      <ul class="py-2" v-for="movie in moviesArray" :key="movie.id">
        <img class="w-50" :src="`${apiImgUrl}${movie.poster_path}`" :alt="movie.title">
        <li>Title: {{movie.title}}</li>
        <li>Original Title: {{movie.original_title}}</li>
        <li>Original Language: <span :class="`fi fi-${changeFlag(movie.original_language)}`"></span></li>
        <li>Vote Average: {{movie.vote_average}}</li>
      </ul>
    </div>
</template>

<script>
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
      apiImgUrl: "https://image.tmdb.org/t/p/w780",
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
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
