<template>
  <div class="container">
    <div class="row">
      <ul v-for="(movie, index) in moviesArray" :key="index">
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
