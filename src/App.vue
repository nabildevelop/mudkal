<template>
  <div id="app">
    <MainCard/>
  </div>
</template>

<script>
import MainCard from './components/MainCard.vue'

export default {
  name: 'app',
  components: {
    MainCard
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
