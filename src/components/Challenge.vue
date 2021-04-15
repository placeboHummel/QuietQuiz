<template>
  <div>
    <div class="tag alignright">{{ questionIndex }}/5</div>
    <div class="title is-5" v-html="question"></div>
  </div>
</template>

<script>
export default {
  name: "Challenge",
  props: {
    question: String,
    questionIndex: Number
  }
};
</script>

<style scoped>
.alignright {
  float: right;
}
</style>
