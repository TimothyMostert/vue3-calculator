<template>
  <div class="calculator">
    <section class="display">
      {{ counter }}
    </section>
    <section class="inputs">
      <div class="default-button" @click="decrementCounter()">-</div>
      <div class="default-button" @click="incrementCounter()">+</div>
    </section>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Calculator",
  setup() {
    let counter = ref(1);

    const incrementCounter = () => {
      counter.value++;
    };

    const decrementCounter = () => {
      if (counter.value > 0) {
        counter.value--;
      }
    };

    return {
      counter,
      incrementCounter,
      decrementCounter,
    };
  },
};
</script>

<style scoped lang="scss">
.calculator {
  padding: 1.5em 1em;
  background: #2c2c2c;
  width: 400px;
  height: 600px;
  .display {
    background-color: beige;
    width: fill-available;
    padding: 0.75em;
    text-align: left;
    font-weight: bold;
    margin-bottom: 0.75em;
    border: 2px solid white;
  }
  .inputs {
    display: flex;
    align-items: center;
    .default-button {
      background: lightgray;
      padding: 0.75em;
      margin-right: 0.75em;
      min-width: 120px;
      border: 2px solid hsl(0, 1%, 27%);
      cursor: pointer;
    }
  }
}
</style>
