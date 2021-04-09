<template>
  <div>
    <div v-for="answer in answers" :key="answer.answers">
      <div v-if="!decisionMade">
        <div class="box title is-6" v-on:click="checkAnswer(answer)">
          {{ answer }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PossibleAnswers",
  props: {
    answers: Array,
    decisionMade: Boolean
  },
  methods: {
    checkAnswer(selectedAnswer) {
      this.$emit("checkAnswer", selectedAnswer);
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
