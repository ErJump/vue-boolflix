<template>
  <div class="container py-5">
    <div class="row">
      <div class="col-6">
        <ul v-for="movie in moviesArray" :key="movie.id">
          <li>Titolo: {{movie.title}}</li>
          <li>Titolo Originale: {{movie.original_title}}</li>
          <li>Lingua: <span :class="`fi fi-${changeFlag(movie.original_language)}`"></span></li>
          <li>Voto: {{movie.vote_average}}</li>
        </ul>
      </div>
      <div class="col-6">
        
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
    }
  },
  methods:{
    changeFlag: function (lang){
      switch (lang) {
        case 'en':
          return 'gb';
      }
      return lang
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
