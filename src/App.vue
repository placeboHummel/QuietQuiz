<template>
  <div class="app">
    <img src="https://i.ibb.co/ZMZShv1/quiz.png" />
    <Challenge :question="question.question" />
    <div class="options">
      <PossibleAnswers :answers="answers" :correctAnswer="correctAnswer" />
    </div>
    <div><Feedback /></div>
    <div>
      <button onClick="window.location.reload();">Nächste Frage</button>
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
      question: null,
      answers: null,
      correctAnswer: null
    };
  },
  created() {
    let random = Math.floor(Math.random() * this.challenges.length);
    this.question = this.challenges[random];
    this.answers = this.challenges[random].answers;
    this.correctAnswer = this.challenges[random].answers[
      this.challenges[random].correct
    ];
  },
  methods: {}
};
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
}

button {
  display: inline-block;
  padding: 0.5em 3em;
  border: 0.16em solid #ffffff;
  margin: 0 0.3em 0.3em 0;
  box-sizing: border-box;
  text-decoration: none;
  text-transform: uppercase;
  font-family: "Roboto", sans-serif;
  font-weight: 400;
  color: black;
  text-align: center;
  transition: all 0.15s;
}

button:hover {
  color: black;
  border-color: #dddddd;
}

button:active {
  color: black;
  border-color: #bbbbbb;
}
</style>
