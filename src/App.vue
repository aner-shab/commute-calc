<template>
  <div id="app">
    <Commute ></Commute>
  </div>
</template>

<script>
import Commute from './components/Commute.vue'
export default {
  name: 'app',
  components: {
      Commute
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
