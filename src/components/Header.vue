<template>
  <b-nav tabs>
    <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
    <b-nav-item disabled>
      <b>Counter {{ numberCorrect }}/{{ numberTotal }}</b>
    </b-nav-item>
  </b-nav>
</template>

<script>
export default {
  props: ["numberCorrect", "numberTotal"],
};
</script>
