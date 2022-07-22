<template>
  <main>
    <div class="container-xxl py-5">
      <div class="row py-3">
        <MovieList :moviesArray="moviesArray" />
      </div>
      <div class="row py-3">
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

<style scoped lang="scss">
  @import "../assets/styles/variables.scss";
  main{
    background-color: $bgMain;
    min-height: 100vh;
    padding-top: 120px;
  }
</style>
