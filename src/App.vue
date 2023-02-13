<template>
  <div class="app">
    Vue Calcul8r
    <CalculatorComp />
  </div>
</template>

<script>
import CalculatorComp from './components/CalculatorComponent.vue'

export default {
  name: 'App',
  components: {
    CalculatorComp
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  
  color: white;
  font-size: 50px;
}
</style>
