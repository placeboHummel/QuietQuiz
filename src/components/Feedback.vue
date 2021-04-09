<template>
  <div>
    <h2 class="right" v-if="questionIsCorrect">Das war richtig!</h2>
    <h2 class="wrong" v-else>Das war leider falsch.</h2>
  </div>
</template>

<script>
export default {
  name: "Feedback",
  props: {
    questionIsCorrect: Boolean
  }
};
</script>

<style scoped></style>
