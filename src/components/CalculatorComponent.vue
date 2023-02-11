<template>
  <div class="calculator">
    <div class="result">
      {{ currentVal || 0 }}
    </div>
    <div class="buttons">
      <button v-for="(btn, i) in buttons" :key="i">{{btn}}</button>
    </div>
    <div class="pastResults">
      Verlauf: {{ pastResults }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorComp',
  data() {
    return {
      currentVal: '',
      buttons: 
      ['C', 'CE', '+', '-',
       '7', '8', '9', '*',
       '4', '5', '6', '/',
       '1', '2', '3', '=',
       '0', '.', '%'],
      pastResults: ''
    }
  }
}
</script>

<style>
.calculator {
  max-inline-size: 22rem;
  overflow: hidden;
  margin: auto;
}
.buttons {
  display: grid;
  align-items: center;
  justify-content: center;
  grid-template-columns: repeat(4, 1fr);
}
</style>
