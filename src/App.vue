<template>
  <div class="app">
    <div class="app-nav">
      <div
        v-for="{ name, component } in pages"
        :key="name"
        class="nav-button"
        @click="currentPage = component"
      >
        {{ name }}
      </div>
    </div>

    <div class="app-main">
      <component v-if="currentPage" :is="currentPage" />
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

import Home from "./components/Home.vue";
import Calculator from "./components/Calculator.vue";
import Slideshow from "./components/Slideshow.vue";
import Tests from "./components/Tests.vue";
import Cart from "./components/Cart.vue";
import Carousel from "./components/Carousel.vue";
import Square from "./components/Square.vue";

const currentPage = ref(Carousel);

const pages = computed(() => [
  {
    name: "Хоумпейдж",
    component: Home,
  },
  {
    name: "Калькулятор",
    component: Calculator,
  },
  {
    name: "Слайдшоу",
    component: Slideshow,
  },
  {
    name: "Тесты",
    component: Tests,
  },
  {
    name: "Корзина",
    component: Cart,
  },
  {
    name: "Карусель",
    component: Carousel,
  },
  {
    name: "Квадрат по кругу",
    component: Square,
  },
]);
</script>

<style lang="scss" scoped>
.app {
  display: flex;
  height: 100%;

  &-nav {
    align-self: center;
  }

  &-main {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-grow: 1;
    margin-left: 2rem;
    padding-left: 2rem;
    border-left: 1px solid hsla(160, 100%, 37%, 0.5);
  }
}
</style>
