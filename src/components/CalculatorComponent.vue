<template>
  <div class="calculator">
    <div class="result">
      {{ currentVal || 0 }}
    </div>
    <div class="buttons">
      <button class="btn"
        :class="[['C', 'CE', '/', '*', '+', '-', '='].includes(btn) ? btn === '=' ? 'equalsBtn' : 'operatorBtn' : '']"
        v-for="(btn, i) in buttons" :key="i" @click="onButtonPress(btn)">{{ btn }}</button>
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
    onButtonPress(btn) {

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
html {
  background-color: rgb(96, 82, 82);
  zoom: 160%;
}

.result {
  margin-top: 10px;
  padding-left: 10px;
  padding-right: 10px;
  text-align: right;
  background-color: #2b2b2b;
  border: 1px solid #5abedc;
  font-size: 25px;
}

.calculator {
  max-inline-size: 25rem;
  overflow: hidden;
  margin: auto;
  font-size: 20px;
  color: rgb(214, 214, 214);
}

.buttons {
  font-size: 20px;
  display: grid;
  align-items: center;
  justify-content: center;
  grid-template-columns: repeat(4, 1fr);
  border: 1px solid #414141;
  margin-bottom: 10px;
}

.btn {
  font-size: 20px;
  background-color: #2b2b2b;
  color: rgb(214, 214, 214);
  border: 1px solid #414141;
  transition: 0.2s;
  height: 50px;
}

.btn:hover {
  background-color: #4B4B4B;
  cursor: pointer;
  border: 2px solid #5abedc;
}

.operatorBtn {
  background-color: #dc8c00;
  color: white;
}

.operatorBtn:hover {
  background-color: #a56d0b;
}

.equalsBtn {
  background-color: green;
  grid-column: 4;
  grid-row: 4 / span 5;
  height: 100px;
}

.equalsBtn:hover {
  background-color: darkgreen;
}
</style>
