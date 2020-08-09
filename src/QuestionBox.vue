<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>{{questionDetails.question}}</template>

      <hr class="my-4" />

      <p v-bind:key="answer" v-for="answer in questionDetails.answerList">
        <b-button size="lg" class="answers" v-on:click="choose">{{answer}}</b-button>
      </p>

      <br />
      <b-button variant="info" href="#" id="previous" v-on:click="previous">Previous</b-button>
      <b-button variant="info" href="#" v-on:click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  name: "QuestionBox",
  props: {
    questionDetails: Object,
    next: Function,
    previous: Function
  },
  methods: {
    choose(e) {
      if (e.target.innerHTML === this.questionDetails.correct_answer) {
        e.target.classList.add("correct");
        setTimeout(()=> {
          e.target.classList.remove("correct");
        }, 1000);
      }else{
        e.target.classList.add("wrong");
        setTimeout(()=> {
          e.target.classList.remove("wrong");
        }, 1000);
      }
    }
  }
};
</script>


<style scoped>
.question-box-container {
  margin: 1%;
  margin-top: 90px;
  text-align: center;
}

.answers {
  width: 90%;
}

#previous {
  margin-right: 1%;
}

.correct {
  background-color: #1b5e20;
}

.wrong {
  background-color: #b71c1c ;
}
</style>