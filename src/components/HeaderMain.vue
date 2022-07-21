<template>
  <div class="bg-dark py-3">
    <div class="container">
      <div class="row justify-content-between">
        <div class="col-2">
          <h1 class="text-white">Header</h1>
        </div>
        <div class="col-3 d-flex align-items-center">
          <SearchBar @search="setSearch"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchBar from './SearchBar.vue';
export default {
  name: 'HeaderMain',
  components: {
    SearchBar,
  },
  data: function () {
    return {
      searchValue: '',
    }
  },
  methods: {
    setSearch: function (search) {
      this.searchValue = search;
      this.sendSearchValue();
    },
    sendSearchValue: function () {
      this.$emit('search', this.searchValue);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  /* *{
    outline: 1px solid red;
  } */
</style>
