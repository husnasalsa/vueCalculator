<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      prev: null,
      current: "",
      operator: null,
      operatorClick: false,
    }
  },
  methods: {
    clear() {
      this.current = ''
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
    },
    percent() {
      this.current = `${parseFloat(this.current/100)}`
    },
    append(number) {
      if(this.operatorClick) {
        this.current = ''
        this.operatorClick = false
      }
      this.current = `${this.current}${number}`
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrev() {
      this.operatorClick =  true
      this.prev = this.current
    },
    divide() {
      this.operator = (a, b) => a/b
      this.setPrev()
    },
    multiply() {
      this.operator = (a, b) => a*b
      this.setPrev()
    },
    subtract() {
      this.operator = (a, b) => a-b
      this.setPrev()
    },
    add() {
      this.operator = (a, b) => a+b
      this.setPrev()
    },
    equal() {
      this.current = `${this.operator(parseFloat(this.prev), parseFloat(this.current))}` 
    }

  },
  name: "vueCalculator"
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
  margin: 0 auto;
  width: 400px;

}
.display {
  grid-column: 1/5;
  background-color: black;
  color: white;
}
.zero {
  grid-column: 1/3;
}
.btn {
  background-color: whitesmoke;
  border: 1px solid #333;
}
.operator {
  background-color: orange;
  color: white;
}
</style>
