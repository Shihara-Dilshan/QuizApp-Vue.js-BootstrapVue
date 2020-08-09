<template>
  <div id="app">
    <Navbar />
    <b-container class="bv-example-row">
      <b-row sm="6" offset="3">
        <b-col>
          <QuestionBox v-if="questions.length > 0" v-bind:questionDetails="questions[index]" v-bind:next="next" />
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
  methods:{
    next(){
      this.index < 9 ? this.index++ : console.log("There are no any questions left");
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
      return {
        category: question.category,
        type: question.type,
        difficulty: question.difficulty,
        question: question.question,
        correct_answer: question.correct_answer,
        incorrect_answers: question.incorrect_answers
      };
    });

    this.questions = questions;
    
  }
};
</script>

<style>
</style>
