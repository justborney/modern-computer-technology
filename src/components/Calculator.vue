<template>
  <div class="calculator">
    <div class="display">{{ display }}</div>

    <div class="buttons">
      <template v-for="({ value, event }, index) in buttons" :key="index">
        <button @click="event">{{ value }}</button>
      </template>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const display = ref(0);
const isFirstValue = ref(true);

const buttons = computed(() => [
  {
    value: "1",
    event: () => addValue(1),
  },
  {
    value: "2",
    event: () => addValue(2),
  },
  {
    value: "3",
    event: () => addValue(3),
  },
  {
    value: "+",
    event: () => addOperator("+"),
  },
  {
    value: "4",
    event: () => addValue(4),
  },
  {
    value: "5",
    event: () => addValue(5),
  },
  {
    value: "6",
    event: () => addValue(6),
  },
  {
    value: "-",
    event: () => addOperator("-"),
  },
  {
    value: "7",
    event: () => addValue(7),
  },
  {
    value: "8",
    event: () => addValue(8),
  },
  {
    value: "9",
    event: () => addValue(9),
  },
  {
    value: "/",
    event: () => addOperator("/"),
  },
  {
    value: "C",
    event: () => (display.value = 0),
  },
  {
    value: "0",
    event: () => addValue(0),
  },
  {
    value: "=",
    event: () => calculate(),
  },
  {
    value: "*",
    event: () => addOperator("*"),
  },
]);

const addValue = (value) => {
  if (isFirstValue.value || display.value === 0) {
    display.value = value;
  } else {
    display.value = display.value + value.toString();
  }

  isFirstValue.value = false;
};

const addOperator = (operator) => (display.value += operator);
const calculate = () => (display.value = eval(display.value));
</script>

<style lang="scss" scoped>
.calculator {
  display: flex;
  flex-direction: column;

  .display {
    background-color: #f2f2f2;
    color: #282828;
    margin-bottom: 8px;
    padding: 0 4px;
    text-align: right;
  }

  .buttons {
    display: grid;
    grid-template-columns: 40px 40px 40px 40px;
    grid-template-rows: 40px 40px 40px 40px;
    gap: 4px;
  }

  button {
    background-color: hsla(160, 100%, 37%, 0.8);
    border: none;
    font-size: 2rem;
    cursor: pointer;

    &:active {
      background-color: #282828;
      color: rgba(235, 235, 235, 0.64);
    }
  }
}
</style>
