<template>
  <main>
    <div class="container py-5">
      <div class="row">
        <MovieList :moviesArray="moviesArray" />
        <TvSerieList :seriesArray="seriesArray" />
      </div>
    </div>
  </main>
</template>

<script>
import MovieList from './MovieList.vue';
import TvSerieList from './TvSerieList.vue';
export default {
    name: "ContentMain",
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
    components: {
    MovieList,
    TvSerieList
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "../assets/styles/variables.scss";
  main{
    background-color: $bgMain;
    min-height: calc(100vh - 100px);
  }
</style>
