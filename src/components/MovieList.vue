<template>
    <div class="col-12">
      <h2 class="text-white">Movies</h2>
      <div class="row">
        <div class="col-3 ms_card py-2 position-relative" v-for="movie in moviesArray" :key="movie.id">
          <img class="w-100" v-if="movie.poster_path == null || movie.poster == ''" src="http://www.movienewz.com/img/films/poster-holder.jpg" :alt="movie.name">
          <img v-else class="w-100" :src="`${apiImgUrl}${movie.poster_path}`" :alt="movie.name">
          <div class="ms_backcard">
            <img class="ms_img_back " v-if="movie.poster_path == null" src="http://www.movienewz.com/img/films/poster-holder.jpg" :alt="movie.name">
            <img v-else class="ms_img_back" :src="`${apiImgUrl}${movie.poster_path}`" :alt="movie.name">
            <ul>
              <li>Title: {{movie.title}}</li>
              <li>Original Title: {{movie.original_title}}</li>
              <li>Original Language: <span :class="`fi fi-${changeFlag(movie.original_language)}`"></span></li>
              <li>Vote Average: 
                <i v-for="vote in getVoteAverage(movie.vote_average)" :key="vote" class="fa-solid fa-star"></i>
                <span v-if="movie.vote_average == 0">-</span> 
              </li>
            </ul>
          </div>
        </div>
      </div>
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
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
    height: 70%;
  }
  
</style>
