<template>
  <div id="app">
    <Header />
    <b-container class="bv-example-row" py="5">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox />
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
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10", {
      method: "get",
    }).then((response) => {
      console.log(response.json());
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
