<template>
  <div class="columns is-centered">
    <div class="column is-half has-text-centered">
      <img src="https://i.ibb.co/ZMZShv1/quiz.png" />

      <Challenge
        :question="question.question"
        :class="questionIndex === 5 ? 'hide' : 'show'"
        :questionIndex="questionIndex"
      />

      <br />

      <div class="options">
        <PossibleAnswers
          :decisionMade="decisionMade"
          :answers="answers"
          @checkAnswer="checkAnswer"
          :class="questionIndex === 5 ? 'hide' : 'show'"
        />
      </div>

      <div>
        <Feedback v-if="decisionMade" :questionIsCorrect="questionIsCorrect" />
      </div>

      <div>
        <button
          class="button is-fullwidth"
          v-on:click="next()"
          v-if="decisionMade"
        >
          Weiter
        </button>
      </div>

      <div
        class="notification is-primary"
        v-on:click="newGame()"
        v-if="questionIndex === 5"
      >
        Spiel beendet!
        <br />
        <br />
        Klick hier für eine neue Runde.
      </div>
    </div>
  </div>
</template>

<script>
import Challenge from "./components/Challenge.vue";
import PossibleAnswers from "./components/PossibleAnswers.vue";
import Feedback from "./components/Feedback.vue";

export default {
  name: "App",
  components: {
    Challenge,
    PossibleAnswers,
    Feedback
  },
  data() {
    return {
      challenges: [
        {
          question: "Wie viele Einwoher hat Hamburg?",
          answers: ["1-2 Millionen", "2-3 Millionen"],
          correct: 0
        },
        {
          question: "Wie heißt der Hamburger Bürgermeister?",
          answers: ["Olaf Scholz", "Peter Tschentscher"],
          correct: 1
        },
        {
          question: "Wie viele Brücken hat Hamburg?",
          answers: ["1750", "2500"],
          correct: 1
        },
        {
          question: "Was bedeutet „Covid“?",
          answers: [
            "Challenging obstructive vital disorder",
            "Coronavirus disease"
          ],
          correct: 1
        },
        {
          question: "Wo wurde TV-Koch Tim Mälzer geboren?",
          answers: ["Elmshorn", "Eimsbüttel"],
          correct: 0
        },
        {
          question:
            "Wo trat die erste bestätigte Infektion außerhalb Chinas auf?",
          answers: ["Thailand", "Japan"],
          correct: 0
        },
        {
          question:
            "5G schafft die fünffache Geschwindigkeit des bisherigen Datenverkehrs.",
          answers: ["Stimmmt", "Stimmt nicht"],
          correct: 1
        },
        {
          question: "Was wurde früher auf der Reeperbahn hergestellt?",
          answers: ["Schwerter", "Seile"],
          correct: 1
        }
      ],
      questionIsCorrect: false,
      decisionMade: false,
      question: null,
      answers: null,
      correctAnswer: null,
      questionIndex: 0
    };
  },
  created() {
    this.newGame();
    this.next();
  },
  methods: {
    checkAnswer(selectedAnswer) {
      if (this.decisionMade === false) {
        if (this.correctAnswer === selectedAnswer) {
          this.questionIsCorrect = true;
        } else {
          this.questionIsCorrect = false;
        }

        this.decisionMade = true;
      }
    },
    next() {
      this.questionIndex++;
      this.question = this.challenges[this.questionIndex];
      this.answers = this.challenges[this.questionIndex].answers;
      this.correctAnswer = this.challenges[this.questionIndex].answers[
        this.challenges[this.questionIndex].correct
      ];
      this.decisionMade = false;
    },
    newGame() {
      this.challenges = this.challenges.sort(() => Math.random() - 0.5);
      this.questionIndex = 0;
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
