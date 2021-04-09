<template>
  <div>
    <div v-for="answer in answers" :key="answer.answers">
      <div class="">
        <div class="box">
          <div class="title is-5">{{ answer }}</div>
          <p>
            <button class="button" v-on:click="checkAnswer(answer)">
              Wählen
            </button>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PossibleAnswers",
  props: {
    answers: Array
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
  padding: 3%;
}
</style>
