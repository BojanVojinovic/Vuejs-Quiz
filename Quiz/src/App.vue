<template>
  <div id="app">
    <h1>{{ quizTitle }}</h1>
    <Questions :data="data" />
    <AddQuestion />
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import AddQuestion from "./components/AddQuestion.vue";

export default {
  name: "app",
  components: {
    Questions,
    AddQuestion
  },
  data() {
    return {
      quizTitle: "Lemis Quiz",
      data: [
        {
          question: "Koliko para?",
          answers: ["10e", "20e", "nema"],
          correctAnswer: "10e"
        },
        {
          question: "Koliko para? 2",
          answers: ["10e", "20e 1", "nema 1"],
          correctAnswer: "10e"
        },
        {
          question: "Koliko para? 3",
          answers: ["10e 2", "20e 2", "nema 2"],
          correctAnswer: "nema 2"
        }
      ]
    };
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  position: relative;
}
h1 {
  color: #2c3e50;
  font-size: 60px;
  line-height: 60px;
}
</style>
