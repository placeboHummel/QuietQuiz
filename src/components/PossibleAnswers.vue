<template>
  <div>
    <div class="card" v-for="answer in answers" :key="answer.answers">
      <div class="container">
        <h4>
          <b>{{ answer }}</b>
        </h4>
        <p><button v-on:click="checkAnswer(answer)">Wählen</button></p>
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
button {
  color: #fff !important;
  text-transform: uppercase;
  text-decoration: none;
  background: #407093;
  padding: 20px;
  border-radius: 5px;
  display: inline-block;
  border: none;
  transition: all 0.4s ease 0s;
}

button:hover {
  background: #434343;
  letter-spacing: 2px;
  -webkit-box-shadow: 0px 5px 40px -10px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 5px 40px -10px rgba(0, 0, 0, 0.57);
  box-shadow: 5px 40px -10px rgba(0, 0, 0, 0.57);
  transition: all 0.4s ease 0s;
  cursor: pointer;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  width: auto;
  margin: auto;
  float: none;
  margin-bottom: 25px;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}

.container {
  padding: 2px 16px;
}

.hide {
  display: none;
}

.wrong {
  color: #df75a5;
}

.right {
  color: green;
}
</style>
