<template>
  <div>
    <div v-for="answer in answers" :key="answer">
      <div :class="classes(answer)" @click="checkAnswer(answer)">
        {{ answer }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PossibleAnswers",
  props: {
    answers: Array,
    decisionMade: {
      type: Boolean,
      default: false
    },
    correctAnswer: String
  },
  methods: {
    checkAnswer(selectedAnswer) {
      this.$emit("checkAnswer", selectedAnswer);
    },
    classes(selectedAnswer) {
      let classes = ["box", "title", "is-6"];
      if (this.decisionMade) {
        if (selectedAnswer === this.correctAnswer) {
          classes.push("has-background-success");
        } else {
          classes.push("has-background-danger");
        }

        console.log(selectedAnswer);
      }
      return classes;
    }
  }
};
</script>
<style scoped>
.box {
  margin-bottom: 1rem;
  cursor: pointer;
}
</style>
