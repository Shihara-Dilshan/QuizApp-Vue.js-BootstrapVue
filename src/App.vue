<template>
  <div id="app">
    <Navbar v-bind:qsNo="index" />
    <b-container class="bv-example-row">
      <b-row sm="6" offset="3">
        <b-col>
          <QuestionBox
            v-if="questions.length > 0"
            v-bind:questionDetails="questions[index]"
            v-bind:next="next"
            v-bind:previous="previous"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Navbar from "./Navbar.vue";
import QuestionBox from "./QuestionBox.vue";

export default {
  name: "App",
  components: {
    Navbar,
    QuestionBox
  },
  methods: {
    next() {
      this.index < 9
        ? this.index++
        : console.log("There are no any questions left");

      let QSBox = document.getElementById("QS");
      QSBox.style.display = "none";
      setTimeout(() => {
        QSBox.style.display = "block";
      }, 100);
    },
    previous() {
      this.index > 0
        ? this.index--
        : console.log("This is the very first question");
        
      let QSBox = document.getElementById("QS");
      QSBox.style.display = "none";
      setTimeout(() => {
        QSBox.style.display = "block";
      }, 100);
    },
    randomNumber() {
      return Math.ceil(Math.random() * 4);
    }
  },
  data() {
    return {
      questions: [],
      index: 0
    };
  },
  async mounted() {
    const apiCall = await fetch(
      "https://opentdb.com/api.php?amount=10&type=multiple"
    );
    const result = await apiCall.json();
    const questions = result.results.map(question => {
      let answer = [...question.incorrect_answers];
      answer.splice(this.randomNumber(), 0, question.correct_answer);

      return {
        category: question.category,
        type: question.type,
        difficulty: question.difficulty,
        question: question.question,
        correct_answer: question.correct_answer,
        incorrect_answers: question.incorrect_answers,
        answerList: answer
      };
    });

    this.questions = questions;
  }
};
</script>

<style>
.test {
  -webkit-animation: fadein 1s; /* Safari, Chrome and Opera > 12.1 */
  -moz-animation: fadein 1s; /* Firefox < 16 */
  -ms-animation: fadein 1s; /* Internet Explorer */
  -o-animation: fadein 1s; /* Opera < 12.1 */
  animation: fadein 1s;
}

@keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Firefox < 16 */
@-moz-keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Safari, Chrome and Opera > 12.1 */
@-webkit-keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Internet Explorer */
@-ms-keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Opera < 12.1 */
@-o-keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
