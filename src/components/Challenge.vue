<template>
  <h3>{{ question }}</h3>
</template>

<script>
export default {
  name: "Challenge",
  props: {
    question: String
  }
};
</script>

<style scoped>
h1 {
  margin: 2rem;
}
</style>
