<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template #lead>
        {{ question.question }}
      </template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item v-for="(answer, index) in answers" :key="index">
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

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
      answers.push(this.question.correct_answer);
      return answers;
    },
  },
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}
.btn {
  margin: 0 15px;
  width: 10%;
}
</style>
