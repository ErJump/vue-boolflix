<template>
  <div>
    <input v-model.trim="inputText" type="text" placeholder="search...">
    <button @click="sendInputText">Search</button>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data: function () {
    return {
      inputText: '',
    }
  },
  methods: {
    sendInputText: function () {
      this.$emit('search', this.inputText);
      this.inputText = '';
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
