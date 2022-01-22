<template>
  <div class="calculator">
    <section class="display">
      {{ displayValue }}
    </section>
    <section class="brand">
      <h3>
        Timulator 9000 - e<span class="brand__highlight">X</span>treme edition
      </h3>
    </section>
    <section class="inputs">
      <div class="default-button grey" @click="updateInput('1')">1</div>
      <div class="default-button grey" @click="updateInput('2')">2</div>
      <div class="default-button grey" @click="updateInput('3')">3</div>
      <div class="default-button red" @click="applyOperator('*')">*</div>
      <div class="default-button grey" @click="updateInput('4')">4</div>
      <div class="default-button grey" @click="updateInput('5')">5</div>
      <div class="default-button grey" @click="updateInput('6')">6</div>
      <div class="default-button red" @click="applyOperator('-')">-</div>
      <div class="default-button grey" @click="updateInput('7')">7</div>
      <div class="default-button grey" @click="updateInput('8')">8</div>
      <div class="default-button grey" @click="updateInput('9')">9</div>
      <div class="default-button red" @click="applyOperator('+')">+</div>
      <div class="default-button grey" @click="updateInput('0')">0</div>
      <div class="default-button grey" @click="updateInput('.')">.</div>
      <div class="default-button grey" @click="clear()">C</div>
      <div class="default-button orange" @click="equals()">=</div>
    </section>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Calculator",
  setup() {
    let displayValue = ref("0");
    let currentValue = ref("0");
    let totalValue = undefined;
    const operators = ["-", "+", "*", "/"];
    let operationString = ref("");

    const clear = () => {
      currentValue.value = "0";
      displayValue.value = "0";
      totalValue = undefined;
      operationString.value = "";
    };

    const updateInput = (val) => {
      if (totalValue && !operators.includes(operationString.value.slice(-1))) {
        clear();
      }
      if (val === "0" && currentValue.value === "0") {
        return;
      } else if (currentValue.value === "0") {
        currentValue.value = val;
      } else {
        currentValue.value = currentValue.value + val;
      }
      displayValue.value = currentValue.value;
    };

    const applyOperator = (operator) => {
      if (!operationString.value) {
        operationString.value =
          operationString.value + currentValue.value + operator;
      } else {
        operationString.value = operationString.value + operator;
      }
      currentValue.value = "0";
    };

    const equals = () => {
      operationString.value = operationString.value + currentValue.value;
      currentValue.value = "0";
      console.log(operationString.value);
      console.log(currentValue.value);
      let evaluatedOperationString = eval(operationString.value);
      totalValue = evaluatedOperationString;
      displayValue.value = evaluatedOperationString.toString();
      operationString.value = evaluatedOperationString.toString();
    };

    return {
      displayValue,
      currentValue,
      operationString,
      updateInput,
      clear,
      applyOperator,
      equals,
    };
  },
};
</script>

<style scoped lang="scss">
.calculator {
  padding: 1.8em 1.2em;
  background: #2d2d2d;
  width: 340px;
  height: 400px;
  border-radius: 16px;
  border: 4px solid #796f6c;
  .display {
    background-color: #d7e0e3;
    width: stretch;
    padding: 0.75em;
    text-align: right;
    font-weight: bold;
    margin-bottom: 0.75em;
    border: 2px solid white;
    box-shadow: inset 0 0 10px #000000;
  }
  .brand {
    text-align: left;
    line-height: 1;
    color: whitesmoke;
    font-size: 0.8rem;
    .brand__highlight {
      color: #ff9933;
    }
  }
  .inputs {
    display: flex;
    flex-wrap: wrap;
    flex-wrap: wrap;
    height: 300px;
    align-items: center;
    justify-content: space-around;
    margin-top: 40px;
    .default-button {
      width: 20%;
      height: 40px;
      border: none;
      border-radius: 8px;
      margin-right: 7px;
      cursor: pointer;
      border-top: 2px solid transparent;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.4rem;
      font-weight: bold;
    }
    .grey {
      color: white;
      background-color: #6e6760;
      border-bottom: black 2px solid;
      border-top: 2px #6e6760 solid;
    }
    .grey:active {
      border-top: black 2px solid;
      border-bottom: #6e6760 2px solid;
    }
    .red {
      color: white;
      background-color: #ff4561;
      border-bottom: black 2px solid;
      border-top: 2px #ff4561 solid;
    }
    .red:active {
      border-top: black 2px solid;
      border-bottom: #ff4561 2px solid;
    }
    .orange {
      color: white;
      background-color: #ff9933;
      border-bottom: black 2px solid;
      border-top: 2px #ff9933 solid;
    }
    .orange:active {
      border-top: black 2px solid;
      border-bottom: #ff9933 2px solid;
    }
  }
}
</style>
