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
  data() {
    return {
      selected: String
    };
  },
  methods: {
    checkAnswer(selectedAnswer) {
      this.$emit("checkAnswer", selectedAnswer);
      this.selected = selectedAnswer;
    },
    classes(answer) {
      let classes = ["box", "title", "is-6"];
      if (this.decisionMade) {
        if (answer === this.correctAnswer) {
          classes.push("has-background-success");
        } else if (answer === this.selected) {
          classes.push("has-background-danger");
        }
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
