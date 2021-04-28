<template>
  <div id="app">
    <Header
      :numberCorrectAnswers="numberCorrectAnswers"
      :numberTotalAnswers="numberTotalAnswers"
    />
    <b-container class="bv-example-row my-5">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length"
            :question="questions[index]"
            :next="next"
            :increment="increment"
            :indexControl="index"
          />
        </b-col>
      </b-row>
    </b-container>
    <QuestionBox />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {
  name: "App",
  components: {
    QuestionBox,
    Header,
  },
  data() {
    return {
      questions: [],
      index: 0,
      numberCorrectAnswers: 0,
      numberTotalAnswers: 0,
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numberCorrectAnswers++;
      }
      this.numberTotalAnswers++;
    },
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10", {
      method: "get",
    })
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
