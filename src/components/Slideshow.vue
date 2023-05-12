<template>
  <div class="slideshow">
    <button @click="move(-1)">Туда</button>

    <div class="slides">
      <template v-for="(imagePath, index) in slides">
        <img :key="index" v-if="index === active" :src="imagePath" />
      </template>
    </div>

    <button @click="move(1)">Сюда</button>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const active = ref(1);

const slides = computed(() => [
  "Peepo_Pepe-512px-4.gif",
  "Peepo_Pepe-512px-11.gif",
  "Peepo_Pepe-512px-14.gif",
  "Peepo_Pepe-512px-16.gif",
  "Peepo_Pepe-512px-18.gif",
  "Peepo_Pepe-512px-42.gif",
]);

const move = (amount) => {
  let newActive;
  const newIndex = active.value + amount;

  if (newIndex > slides.value.length - 1) newActive = 1;
  if (newIndex === -1) newActive = slides.value.length - 1;
  active.value = newActive || newIndex;
};
</script>

<style lang="scss" scoped>
.slideshow {
  display: flex;
  align-items: center;
  justify-content: space-around;
  width: 100%;

  button {
    background-color: hsla(160, 100%, 37%, 0.8);
    padding: 4px 12px;
    border: none;
    cursor: pointer;
    font-size: 2rem;

    &:active {
      background: #282828;
      color: rgba(235, 235, 235, 0.64);
    }
  }

  .slides {
    font-size: 40px;
    display: flex;
    height: 100%;
    width: 512px;
    align-items: center;
    justify-content: center;
    font-weight: bold;
  }
}
</style>
