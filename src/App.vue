<template>
  <div class="columns is-centered">
    <div class="column is-half has-text-centered">
      <img src="https://i.ibb.co/ZMZShv1/quiz.png" />

      <h1 class="title is-1" v-if="!this.api_challenges">
        <img src="./assets/giphy.gif" />
      </h1>

      <div v-if="this.api_challenges">
        <Challenge
          :question="api_question.question"
          :class="questionIndex === 6 ? 'hide' : 'show'"
          :questionIndex="questionIndex"
        />
        <hr />

        <div v-if="questionIndex < 6">
          <Answer
            v-for="answer in api_question.answers"
            :key="answer"
            :answer="answer"
            :is-correct="answer === api_question.correctAnswer"
            @click="checkAnswer"
          />
        </div>
        <br />
        <div v-if="decisionMade">
          <div v-if="questionIsCorrect" style="color: green">
            Du liegst richtig.
          </div>
          <div v-else style="color: red">Du liegst leider daneben.</div>
        </div>
        <br />

        <button
          class="button is-fullwidth"
          v-on:click="next()"
          v-if="decisionMade && questionIndex < 6"
        >
          Weiter
        </button>

        <br />
        <div
          class="button is-primary"
          v-on:click="newGame()"
          v-if="questionIndex === 6"
        >
          Spiel beendet! Neue Runde?
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Challenge from "./components/Challenge.vue";
import Answer from "./components/Answer.vue";

export default {
  name: "App",
  components: {
    Challenge,
    Answer
  },
  data() {
    return {
      decisionMade: false,
      questionIndex: 0,
      questionIsCorrect: false,

      // oder als leeres Array?
      api_challenges: undefined
    };
  },
  created() {
    this.next();

    // TODOS:
    // - Refactoring gedanklich erneut durchgehen, Nachvollziehbarkeit sicherstellen
    // - next() Methode reparieren
    // - die stelle der richtigen Antwort soll zufällig vergeben werden

    axios
      .get(
        "https://opentdb.com/api.php?amount=10&category=9&difficulty=easy&type=multiple"
      )
      .then(response => {
        this.api_challenges = response.data.results;
      });
  },
  computed: {
    api_question() {
      if (!this.api_challenges) {
        return null;
      }
      const question = this.api_challenges[this.questionIndex];
      return {
        question: question.question,
        answers: question.incorrect_answers
          .concat(question.correct_answer)
          .sort(() => Math.random() - 0.5),
        correctAnswer: question.correct_answer
      };
    }
  },
  methods: {
    checkAnswer(isCorrectAnswer) {
      console.log(isCorrectAnswer);
      if (this.decisionMade === false) {
        this.questionIsCorrect = isCorrectAnswer;
        this.decisionMade = true;
      }
    },
    next() {
      this.questionIndex++;
      this.questionIsCorrect = false;
      this.decisionMade = false;
    },
    newGame() {
      this.questionIndex = 1;
      this.questionIsCorrect = false;
      this.decisionMade = false;
      this.api_challenges = undefined;

      axios
        .get(
          "https://opentdb.com/api.php?amount=10&category=9&difficulty=easy&type=multiple"
        )
        .then(response => {
          this.api_challenges = response.data.results;
        });
    }
  }
};
</script>

<style>
.column.is-half {
  margin: 1rem;
}

img {
  margin-bottom: 1rem;
}

.show {
  display: block;
}

.hide {
  display: none;
}
</style>
