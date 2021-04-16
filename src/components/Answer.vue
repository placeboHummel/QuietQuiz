<template>
  <div :class="classes()" @click="answerSelected" v-html="answer"></div>
</template>

<script>
export default {
  name: "Challenge",
  props: {
    answer: null,
    isCorrect: {
      type: Boolean,
      default: false
    },
    decisionMade: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      selected: String
    };
  },
  methods: {
    answerSelected() {
      this.$emit("click", this.isCorrect);
      if (this.decisionMade === false) {
        this.selected = this.answer;
      }
    },
    classes() {
      let classes = ["button", "is-fullwidth", "is-dark"];
      if (this.decisionMade) {
        if (this.isCorrect) {
          classes.push("is-success");
        } else if (this.selected === this.answer) {
          classes.push("is-danger");
        }
      }

      return classes;
    }
  }
};
</script>

<style scoped>
.box {
  cursor: pointer;
}

.button {
  margin-bottom: 1rem;
}
</style>
