<template>
  <div class="carousel">
    <div class="container">
      <div class="cards_wrapper">
        <div
          v-for="(card, index) in cards"
          :key="index"
          class="angle_wrapper"
          :style="{ transform: `rotate(${card.deg}deg)` }"
        >
          <div class="card" :style="{ transform: `rotate(-${card.deg}deg)` }">
            {{ card.emoji }}
          </div>
        </div>
      </div>
    </div>

    <div :style="{ margin: 20 }">
      <button
        @click="
          () => {
            isRotate = true;
            handleRotate();
          }
        "
        :style="{ margin: '20px' }"
      >
        Запустить!
      </button>

      <button
        @click="
          () => {
            isRotate = false;
            stop();
          }
        "
        :style="{ margin: '20px' }"
      >
        Остановить!
      </button>
    </div>
  </div>
</template>

<script setup>
import { watchEffect, ref } from "vue";

const isRotate = ref(false);
const cards = ref([
  {
    emoji: "🤣",
    deg: 360,
  },
  {
    emoji: "😊",
    deg: 435,
  },
  {
    emoji: "🤗",
    deg: 500,
  },
  {
    emoji: "🤮",
    deg: 285,
  },
  {
    emoji: "😆",
    deg: 220,
  },
]);

const handleRotate = () => {
  const newCards = cards.value.map((card) => {
    return {
      ...card,
      deg: card.deg + 15,
    };
  });

  cards.value = newCards;
};

const stop = watchEffect(() => {
  if (!isRotate.value) return;

  var startInterval = setInterval(() => {
    if (isRotate.value) {
      handleRotate();
    }
  }, 200);

  return () => clearInterval(startInterval);
});
</script>

<style lang="scss" scoped>
.cards_wrapper {
  position: relative;
  height: 485px;
  width: 485px;
}

.cards_wrapper::before {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: calc(100% - 66px);
  height: calc(100% - 66px);
  box-sizing: border-box;
  border-radius: 50%;
  border: 3px dashed #d5e1ec;
}

.angle_wrapper {
  position: absolute;
  left: calc(50% - 50px);
  height: 50%;
  transform-origin: 50% 100%;
  transition: transform 0.2s linear;
}

.card {
  position: relative;
  display: inline-flex;
  flex-flow: column nowrap;
  justify-content: start;
  align-items: center;
  text-align: center;
  height: 100px;
  width: 100px;
  transform-origin: 50% 33px;
  transition: transform 0.2s linear;
  font-size: 3rem;
}

button {
  background-color: hsla(160, 100%, 37%, 0.8);
  border: none;
  padding: 4px 12px;
  font-size: 2rem;
  cursor: pointer;

  &:active {
    background-color: #282828;
    color: rgba(235, 235, 235, 0.64);
  }
}
</style>
