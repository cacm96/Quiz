<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template #lead>
        {{ question.question }}
      </template>

      <hr class="my-4" />

      <p v-for="answer in answers" :key="answer">
        answer
      </p>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: {
    question: Object,
    next: Function,
  },
  computed: {
    answers() {
      let answers = [...this.question.incorrect_answers];
      return answers.push(this.question.correct_answer);
    },
  },
};
</script>
