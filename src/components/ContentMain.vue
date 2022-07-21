<template>
  <div class="container py-5">
    <div class="row">
      <ul v-for="movie in moviesArray" :key="movie.id">
        <li>Titolo: {{movie.title}}</li>
        <li>Titolo Originale: {{movie.original_title}}</li>
        <li>Lingua: {{movie.original_language}}</li>
        <li>Voto: {{movie.vote_average}}</li>
      </ul>
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
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
