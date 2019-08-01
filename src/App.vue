<template>
  <div id="app">
    <Dew/>
  </div>
</template>

<script>
import Dew from './components/Dew.vue'

export default {
  name: 'app',
  components: {
    Dew
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
