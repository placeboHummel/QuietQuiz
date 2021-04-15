<template>
  <div class="box has-background-warning" @click="answerSelected">
    {{ answer }}
  </div>
</template>

<script>
export default {
  name: "Challenge",
  props: {
    answer: null,
    isCorrect: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    answerSelected() {
      this.$emit("click", this.isCorrect);
    }
  }
};
</script>

<style scoped></style>
