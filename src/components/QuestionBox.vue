<template>
  <div class="question-box-container my-5">
    <b-jumbotron>
      <template #lead>
        {{ question.question }}
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswer"
          :key="index"
          @click.prevent="selectAnswer(index)"
          :class="answerClasses(index)"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <b-button
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
        >Submit</b-button
      >
      <b-button
        variant="success"
        @click="next"
        :disabled="selectedIndex === null || !answered || indexControl >= 9"
        >Next</b-button
      >
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  props: {
    question: Object,
    next: Function,
    indexControl: Number,
    increment: Function,
  },
  data() {
    return {
      selectedIndex: null,
      shuffledAnswer: [],
      correctIndex: null,
      answered: false,
    };
  },
  watch: {
    question: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.shuffleAnswer();
        this.answered = false;
      },
    },
  },
  computed: {
    answers() {
      let answers = [...this.question.incorrect_answers];
      answers.push(this.question.correct_answer);
      return answers;
    },
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    answerClasses(index) {
      let answer = "";
      if (!this.answered && this.selectedIndex === index) answer = "selected";
      if (this.answered && this.correctIndex === index) answer = "correct";
      if (
        this.answered &&
        this.correctIndex !== index &&
        this.selectedIndex === index
      )
        answer = "incorrect";
      return answer;
    },
    submitAnswer() {
      let isCorrect = false;

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },
    shuffleAnswer() {
      let answers = [
        ...this.question.incorrect_answers,
        this.question.correct_answer,
      ];
      this.shuffledAnswer = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswer.indexOf(
        this.question.correct_answer
      );
    },
  },
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}
.list-group-item:hover {
  background: #eee;
  cursor: pointer;
}
.btn {
  width: 20%;
  margin: 0 15px;
}

.selected {
  background-color: lightblue;
}
.correct {
  background-color: lightgreen;
}
.incorrect {
  background-color: lightsalmon;
}
</style>
