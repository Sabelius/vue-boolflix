<template>
  <div id="app">
    <All />
  </div>
</template>

<script>
import All from './components/All.vue'


export default {
  name: 'App',
  components: {
    All,
  
  }
}
</script>

<style lang="scss">
@import "./style/general.scss";


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
