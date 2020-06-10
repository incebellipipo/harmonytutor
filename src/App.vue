<template>
  <div id="app">
    <ruler/>
  </div>
</template>

<script>
import Ruler from './components/Ruler.vue'

export default {
  name: 'app',
  components: {
    Ruler
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
