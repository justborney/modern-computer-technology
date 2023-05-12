<template>
  <div class="tests">
    <div v-if="completed" class="result">{{ result }}</div>

    <template v-else>
      <div class="controls">
        <button @click="completed = true">Завершить</button>
      </div>

      <div class="display">
        <div class="title">{{ currentQuestion.title }}</div>

        <div class="variants">
          <button
            v-for="variant in currentQuestion.variants"
            :class="[
              'variant',
              { active: currentQuestion.typedAnswer === variant },
            ]"
            @click="selectVariant(variant)"
          >
            {{ variant }}
          </button>
        </div>
      </div>

      <div class="questions">
        <button
          v-for="question in questions"
          @click="currentQuestionId = question.id"
        >
          {{ question.id }}
        </button>
      </div>
    </template>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const completed = ref(false);
const currentQuestionId = ref(1);
const questions = ref([
  {
    id: 1,
    title: "Первый элемент в таблице Менделеева — это…",
    variants: ["Железо", "Магний", "Водород"],
    answer: "Водород",
    typedAnswer: "",
  },
  {
    id: 2,
    title: "Кто открыл Америку?",
    variants: ["Васко да Гама", "Христофор Колумб", "Диего Колон"],
    answer: "Христофор Колумб",
    typedAnswer: "",
  },
  {
    id: 3,
    title: "Какая планета расположена ближе всех к Солнцу?",
    variants: ["Меркурий", "Венера", "Марс"],
    answer: "Меркурий",
    typedAnswer: "",
  },
  {
    id: 4,
    title: "Сколько клеток на шахматной доске?",
    variants: ["16", "64", "32"],
    answer: "64",
    typedAnswer: "",
  },
]);

const result = computed(() => {
  const totalCorrectAnswers = questions.value.filter(
    ({ answer, typedAnswer }) => answer === typedAnswer
  );

  return `Всего правильных ответов ${totalCorrectAnswers.length} из ${questions.value.length}`;
});

const currentQuestion = computed(() =>
  questions.value.find(({ id }) => id === currentQuestionId.value)
);

const selectVariant = (variant) => {
  questions.value[currentQuestionId.value - 1].typedAnswer = variant;
};
</script>

<style lang="scss" scoped>
.tests {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  height: 100%;
  width: 100%;

  .display {
    font-size: 2rem;

    .variants {
      display: flex;
      flex-direction: column;
      align-items: baseline;
      gap: 4px;
    }
  }

  .questions {
    display: flex;
    gap: 4px;
  }

  .result {
    font-size: 3rem;
  }
}

button {
  background-color: hsla(160, 100%, 37%, 0.8);
  padding: 4px 12px;
  font-size: 2rem;
  border: none;
  cursor: pointer;

  &:active,
  &.active {
    background-color: #282828;
    color: rgba(235, 235, 235, 0.64);
  }
}
</style>
