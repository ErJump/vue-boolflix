<template>
  <header class="ms_bg py-3">
    <div class="container-fluid px-5">
      <div class="row justify-content-between">
        <div class="col-2">
          <img class="w-50" src="../assets/img/boolflix-logo.png" alt="boolflix logo">
        </div>
        <div class="col-3 d-flex align-items-center justify-content-end">
          <SearchBar @search="setSearch"/>
          <img class="ms_avatar rounded-2" src="../assets/img/avatar.png" alt="avatar">
        </div>
      </div>
    </div>
  </header>
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
    //setta la variabile searchValue con il valore passato dalla SearchBar e invoca la funzione di emit
    setSearch: function (search) {
      this.searchValue = search;
      this.sendSearchValue();
    },
    //emit per la variabile searchValue
    sendSearchValue: function () {
      this.$emit('search', this.searchValue);
    }
  }
}
</script>

<style scoped lang="scss">
  @import "../assets/styles/variables.scss";
  header{
    height: 100px;
    position: fixed;
    left: 0;
    right: 0;
    z-index: 20;
  }
  .ms_avatar {
    width: 50px;
    height: 50px;
    margin-left: 10px;
  }
  .ms_bg {
    background-image: linear-gradient($bgHeaderFirst, $bgHeaderSecond);
  }
</style>
