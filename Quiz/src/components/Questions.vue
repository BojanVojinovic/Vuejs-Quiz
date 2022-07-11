<template>
  <div>
    <div v-if="isQuizActive">
      <QuestionCounter
        :currentQuestion="currentQuestion"
        :questionLength="data.length"
      />
      <h2>{{ data[activeQuestion].question }}</h2>
      <p
        class="answers"
        :style="{ cursor: disableQuestion ? 'not-allowed' : 'pointer' }"
        v-for="(answer, index) in data[activeQuestion].answers"
        :key="answer"
        @click="checkAnswer(index, answer, $event)"
      >
        {{ answer }}
      </p>

      <button class="nextBtn" @click="nextQuestion()">Sledece pitanje</button>
    </div>
    <div v-else>
      <p>Dragi korisnice, hvala Vam na igri!</p>
      <p>Broj tacnih odgovora: {{ correctAnswers }}</p>
      <p>Broj netacnih odgovora: {{ wrongAnswers }}</p>
      <p>
        {{ this.msgForWrong() }}
      </p>
      <button @click="anotherGame()" class="nextBtn">Igraj ponovo</button>
    </div>
  </div>
</template>

<script>
import QuestionCounter from "./QuestionCounter.vue";
export default {
  name: "Questions",
  props: {
    data: Array
  },
  components: {
    QuestionCounter
  },

  data() {
    return {
      isQuizActive: true,
      currentQuestion: 1,
      activeQuestion: 0,
      answeredQuestion: [],
      disableQuestion: false,
      correctAnswers: 0,
      wrongAnswers: 0
    };
  },
  mounted() {
    this.activeQuestion = this.randomQuestion();
    this.answeredQuestion.push(this.activeQuestion);
  },
  methods: {
    msgForWrong() {
      var msg = "";
      switch (this.correctAnswers) {
        case 0:
          msg = "Veze nemas";
          break;
        case 1:
          msg = "A jadan ne bio";
          break;
        case 2:
          msg = "Skoro pa dobro";
          break;
        case 3:
          msg = "Brao majstore";
          break;
        default:
          msg = "sta radis";
          break;
      }
      return msg;
    },
    randomQuestion() {
      var maxIndex = this.data.length;
      console.log(maxIndex, "maxIndex");
      var questionIndex = Math.floor(Math.random() * maxIndex);
      return questionIndex;
    },
    anotherGame() {
      this.isQuizActive = true;
      this.answeredQuestion = [];
      this.activeQuestion = 0;
      this.correctAnswers = 0;
      this.wrongAnswers = 0;
      this.currentQuestion = 1;
      this.disableQuestion = false;
      this.activeQuestion = this.randomQuestion();
      this.answeredQuestion.push(this.activeQuestion);
    },
    nextQuestion() {
      if (this.answeredQuestion.length != this.data.length) {
        this.answeredQuestion.push(this.activeQuestion);
        if (this.activeQuestion == this.data.length - 1) {
          this.activeQuestion = 0;
        } else {
          this.activeQuestion++;
        }
        var answersClass = document.getElementsByClassName("answers");
        this.data.forEach((el, index) => {
          answersClass[index].classList.remove("correct");
          answersClass[index].classList.remove("wrong");
        });
        this.currentQuestion++;

        this.disableQuestion = false;
      } else {
        this.isQuizActive = false;
      }
    },
    checkAnswer(index, answer, event) {
      var correctAnswer = this.data[this.activeQuestion].correctAnswer;

      if (answer === correctAnswer) {
        event.target.classList.add("correct");
        this.correctAnswers++;
      } else {
        event.target.classList.add("wrong");
        this.wrongAnswers++;
        const answersClass = document.getElementsByClassName("answers");
        var answers = this.data[this.activeQuestion].answers;
        const index = answers.findIndex(answer => answer === correctAnswer);
        answersClass[index].classList.add("correct");
      }

      this.disableQuestion = true;
    }
  }
};
</script>

<style lang="scss">
h1 {
  color: #2c3e50;
  font-size: 60px;
  line-height: 60px;
}

.nextBtn {
  background: transparent;
  border: 1px solid green;
  padding: 16px;
  border-radius: 8px;
  margin-top: 20px;
  &:hover {
    background: green;
  }
}

.answers {
  border: 1px solid blue;
  padding: 18px;
  width: 500px;
  margin: 0 auto;
  margin-top: 10px;
  &.correct {
    background: green;
    color: #fff;
  }
  &.wrong {
    background: red;
    color: #fff;
  }
}
</style>
