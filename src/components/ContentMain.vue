<template>
  <div class="container py-5">
    <div class="row">
      <div class="col-6">
        <h2>Movies</h2>
        <ul v-for="movie in moviesArray" :key="movie.id">
          <li>Title: {{movie.title}}</li>
          <li>Original Title: {{movie.original_title}}</li>
          <li>Original Language: <span :class="`fi fi-${changeFlag(movie.original_language)}`"></span></li>
          <li>Vote Average: {{movie.vote_average}}</li>
        </ul>
      </div>
      <div class="col-6">
        <h2>TV Series</h2>
        <ul v-for="serie in seriesArray" :key="serie.id">
          <li>Title: {{serie.name}}</li>
          <li>Original Title: {{serie.original_name}}</li>
          <li>Original Language: <span :class="`fi fi-${changeFlag(serie.original_language)}`"></span></li>
          <li>Vote Average: {{serie.vote_average}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContentMain',
  props: {
    moviesArray: {
      type: Array,
      required: true
    },
    seriesArray: {
      type: Array,
      required: true
    }
  },
  methods:{
    changeFlag: function (lang){
      switch (lang) {
        case 'en':
          return 'gb';
        case 'ja':
          return 'jp';
        case 'ko':
          return 'kr';
      }
      return lang
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
