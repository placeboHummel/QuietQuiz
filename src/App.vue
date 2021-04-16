<template>
  <div class="columns is-centered">
    <div class="column is-half has-text-centered">
      <div class="heading">Smarticus</div>
      <div class="columns is-mobile has-text-centered">
        <div class="column" v-on:click="newGame()">
          <div class="tag is-success newgame">Neues Spiel</div>
        </div>
        <div class="column">
          <div class="tag">{{ index }}</div>
        </div>
        <div class="column">
          <div class="tag">Punkte: {{ points }}</div>
        </div>
      </div>
      <div v-if="!gameOver">
        <h1 class="title is-1" v-if="!this.challenges">
          <img src="./assets/giphy.gif" />
        </h1>

        <div v-if="this.challenges">
          <Challenge
            :question="currentChallenge.question"
            :questionIndex="questionIndex"
          />
          <br />
          <Answer
            v-for="answer in currentChallenge.answers"
            :key="answer"
            :answer="answer"
            :is-correct="answer === currentChallenge.correctAnswer"
            :decisionMade="decisionMade"
            @click="checkAnswer"
          />

          <br />
          <button
            class="button is-light is-fullwidth"
            v-on:click="next()"
            v-if="decisionMade && questionIndex < 6"
          >
            ➔
          </button>
        </div>
      </div>
      <GameOver :points="points" v-if="gameOver" v-on:click="newGame()" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Challenge from "./components/Challenge.vue";
import Answer from "./components/Answer.vue";
import GameOver from "./components/GameOver.vue";

export default {
  name: "App",
  components: {
    Challenge,
    Answer,
    GameOver
  },
  data() {
    return {
      decisionMade: false,
      questionIndex: 0,
      questionIsCorrect: false,
      points: 0,

      // oder als leeres Array?
      challenges: undefined
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
        this.challenges = response.data.results;
      });
  },
  computed: {
    currentChallenge() {
      if (!this.challenges) {
        return null;
      }
      const current_challenge = this.challenges[this.questionIndex];
      return {
        question: current_challenge.question,
        answers: current_challenge.incorrect_answers
          .concat(current_challenge.correct_answer)
          .sort(() => Math.random() - 0.5),
        correctAnswer: current_challenge.correct_answer
      };
    },
    gameOver() {
      if (this.questionIndex >= 6) {
        return true;
      } else {
        return false;
      }
    },
    index() {
      if (this.questionIndex > 5) {
        return "Spielende";
      } else {
        return "Frage " + this.questionIndex + "/5";
      }
    }
  },
  methods: {
    checkAnswer(isCorrectAnswer) {
      if (this.decisionMade === false) {
        this.questionIsCorrect = isCorrectAnswer;
        this.decisionMade = true;

        if (isCorrectAnswer) {
          this.points++;
        }
      }
    },
    next() {
      this.questionIndex++;
      this.questionIsCorrect = false;
      this.decisionMade = false;
    },
    newGame() {
      this.questionIndex = 1;
      this.points = 0;
      this.questionIsCorrect = false;
      this.decisionMade = false;
      this.challenges = undefined;

      axios
        .get(
          "https://opentdb.com/api.php?amount=10&category=9&difficulty=easy&type=multiple"
        )
        .then(response => {
          this.challenges = response.data.results;
        });
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Monoton&display=swap");

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

.heading {
  font-family: "Monoton", cursive;
  font-size: 40px !important;
  margin-bottom: 9rem;
}

.newgame {
  cursor: pointer;
}
</style>
