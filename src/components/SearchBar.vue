<template>
  <div class="w-100 d-flex">
    <button class="ms_button px-2 py-1" @click="sendInputText"><i class="text-white ms_size fa-solid fa-magnifying-glass"></i></button>
    <input class="ms_text_input px-3 py-1" v-model.trim="inputText" type="text" placeholder="search...">
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
 .ms_button{
  padding: 0;
  background-color: transparent;
  border: none;
  align-items: center!important;
  display: flex;
  border-top: 1px solid white;
  border-left: 1px solid white;
  border-bottom: 1px solid white;
 }
 .ms_size{
  font-size: 1.5rem;
 }
 .ms_text_input{
  width: 100%;
  border: none;
  background-color: transparent;
  border-top: 1px solid white;
  border-right: 1px solid white;
  border-bottom: 1px solid white;
  padding: 0;
  font-size: 1.5rem;
  color: white;
  outline: none;
  max-width: 300px;
 }
</style>
