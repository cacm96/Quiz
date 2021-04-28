<template>
  <b-nav tabs>
    <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
    <b-nav-item disabled
      >Counter: {{ numberCorrectAnswers }}/{{ numberTotalAnswers }}</b-nav-item
    >
  </b-nav>
</template>

<script>
export default {
  props: ["numberCorrectAnswers", "numberTotalAnswers"],
};
</script>
