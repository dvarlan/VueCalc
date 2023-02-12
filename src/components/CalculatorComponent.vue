<template>
  <div class="calculator">
    <div class="result">
      {{ currentVal || 0 }}
    </div>
    <div class="buttons">
      <button v-for="(btn, i) in buttons" :key="i" @click="onButtonPress(btn)">{{btn}}</button>
    </div>
    <div class="pastResults" v-if="pastResults.length != 0">
      Past results: {{ pastResults }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorComp',
  data() {
    return {
      currentVal: '',
      result: '',
      buttons: 
      ['C', 'CE', '+', '-',
       '7', '8', '9', '*',
       '4', '5', '6', '/',
       '1', '2', '3', '=',
       '0', '.', '%'],
      pastResults: []
    }
  },
  methods: {
    onButtonPress (btn) {

      if (btn === 'C') {
        this.currentVal = ''
      }

      if (btn === 'CE') {
        this.currentVal = ''
        this.pastResults = []
      }

      if (btn === '=') {
        try {
          this.result = eval(this.currentVal)
          this.appendPastResults(this.result)
          this.currentVal = this.result
        } catch (error) {
          this.currentVal = 'ERROR!'
        }
      }

      if (!['=', 'C', 'CE'].includes(btn)) {
        this.currentVal += btn
      }
    },
    appendPastResults(res) {
      if (this.pastResults.length <= 5) {
        this.pastResults.push(res)
      } else {
        this.pastResults.shift()
        this.pastResults.push(res)
      }
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
