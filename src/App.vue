<template>
  <div id="app">
    <calculator/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Calculator from './components/calculator.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Calculator
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
