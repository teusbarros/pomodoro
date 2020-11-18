<template>
  <div id="app">
    <Barra :percentual="0"></Barra>
  </div>
</template>

<script>
import Barra from './components/Barra.vue'

export default {
  name: 'App',
  components: {
    Barra
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
