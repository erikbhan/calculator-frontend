<template>
  <div class="container">
    <div class="calculator">
      <div class="display">{{ calculatorValue || 0 }}</div>
      <button
        @click="handleButtonPress"
        v-if="calculatorValue === ''"
        class="acc misc"
      >
        AC
      </button>
      <button @click="handleButtonPress" v-else class="acc misc">C</button>
      <button @click="handleButtonPress" class="invert misc">+/-</button>
      <button @click="handleButtonPress" class="percent misc">%</button>
      <button @click="handleButtonPress" class="divide operator">/</button>
      <button @click="handleButtonPress" class="multiply operator">*</button>
      <button @click="handleButtonPress" class="minus operator">-</button>
      <button @click="handleButtonPress" class="plus operator">+</button>
      <button @click="handleButtonPress" class="equals operator">=</button>
      <button @click="handleButtonPress" class="dot">.</button>
      <button @click="handleButtonPress" class="zerozero">00</button>
      <button @click="handleButtonPress" class="zero">0</button>
      <button @click="handleButtonPress" class="one">1</button>
      <button @click="handleButtonPress" class="two">2</button>
      <button @click="handleButtonPress" class="three">3</button>
      <button @click="handleButtonPress" class="four">4</button>
      <button @click="handleButtonPress" class="five">5</button>
      <button @click="handleButtonPress" class="six">6</button>
      <button @click="handleButtonPress" class="seven">7</button>
      <button @click="handleButtonPress" class="eight">8</button>
      <button @click="handleButtonPress" class="nine">9</button>
    </div>
    <ul class="log">
      <li v-for="item in history" :key="item">
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      calculatorValue: "",
      previousCalculatorValue: "",
      operator: "",
      history: [] as string[],
    };
  },
  methods: {
    handleButtonPress(event: Event) {
      let buttonPressed = (event.target as HTMLButtonElement).innerText;

      // Append number
      if (!isNaN(parseInt(buttonPressed))) {
        this.calculatorValue += buttonPressed;
        this.calculatorValue = parseFloat(this.calculatorValue) + "";
      }

      // Append dot
      if (buttonPressed === ".") {
        if (this.calculatorValue.includes(".")) return;
        this.calculatorValue += buttonPressed;
      }

      // Clear all/clear
      if (buttonPressed === "C" || buttonPressed === "AC") {
        this.calculatorValue = "";
        if (buttonPressed === "C") return;
        this.previousCalculatorValue = "";
        this.operator = "";
      }

      // Percent
      if (buttonPressed === "%") {
        this.calculatorValue = parseFloat(this.calculatorValue) / 100 + "";
      }

      // Invert
      if (buttonPressed === "+/-") {
        this.calculatorValue = -parseFloat(this.calculatorValue) + "";
      }

      // Operators
      if (["/", "*", "-", "+"].includes(buttonPressed)) {
        this.operator = buttonPressed;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }

      // Evaluate
      if (buttonPressed === "=") {
        if (this.previousCalculatorValue === "") return;
        let equation =
          this.previousCalculatorValue + this.operator + this.calculatorValue;
        this.calculatorValue = eval(equation);
        equation += "=" + this.calculatorValue;
        this.history.push(equation);
        this.previousCalculatorValue = "";
        this.operator = "";
      }
    },
  },
});
</script>

<style scoped>
button {
  font-size: xx-large;
  color: #ffffff;
  background-color: #313131;
  border: none;
  /* border-radius: 50%; */
}

.misc {
  color: #000000;
  background-color: #9f9f9f;
}

.operator {
  background-color: #f69806;
}

.container {
  height: 88%;
  min-height: 300px;
  display: grid;
  grid-auto-columns: 1fr;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr;
  gap: 0px 0px;
}

.calculator {
  display: grid;
  margin-top: 40px;
  padding: 5px;
  grid-area: 1 / 2 / 2 / 3;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(6, 1fr);
  grid-auto-columns: 1fr;
  gap: 4px 4px;
  grid-auto-flow: row;
  max-height: 600px;
  min-height: 300px;
  max-width: 400px;
  min-width: 200px;
  height: 80%;
  border-radius: 2%;
  background-color: rgba(0, 0, 0, 0.5);
}

.log {
  list-style: none;
  font-size: xx-large;
  max-height: 100%;
  padding: 0;
  grid-area: 1 / 3 / 2 / 4;
  overflow-y: scroll;
  overflow-x: hidden;
  color: white;
  margin: 20px;
  background-color: #313131;
  border-radius: 2%;
}

.log li {
  padding: 10px;
}

.display {
  padding: 4px;
  font-size: xx-large;
  display: flex;
  justify-content: right;
  align-items: center;
  color: #f8f8f2;
  grid-area: 1 / 1 / 2 / 5;
}

.acc {
  grid-area: 2 / 1 / 3 / 2;
}

.invert {
  grid-area: 2 / 2 / 3 / 3;
}

.percent {
  grid-area: 2 / 3 / 3 / 4;
}

.divide {
  grid-area: 2 / 4 / 3 / 5;
}

.multiply {
  grid-area: 3 / 4 / 4 / 5;
}

.minus {
  grid-area: 4 / 4 / 5 / 5;
}

.plus {
  grid-area: 5 / 4 / 6 / 5;
}

.equals {
  grid-area: 6 / 4 / 7 / 5;
}

.dot {
  grid-area: 6 / 3 / 7 / 4;
}

.zerozero {
  grid-area: 6 / 1 / 7 / 2;
}

.zero {
  grid-area: 6 / 2 / 7 / 3;
}

.one {
  grid-area: 5 / 1 / 6 / 2;
}

.two {
  grid-area: 5 / 2 / 6 / 3;
}

.three {
  grid-area: 5 / 3 / 6 / 4;
}

.four {
  grid-area: 4 / 1 / 5 / 2;
}

.five {
  grid-area: 4 / 2 / 5 / 3;
}

.six {
  grid-area: 4 / 3 / 5 / 4;
}

.seven {
  grid-area: 3 / 1 / 4 / 2;
}

.eight {
  grid-area: 3 / 2 / 4 / 3;
}

.nine {
  grid-area: 3 / 3 / 4 / 4;
}
</style>
