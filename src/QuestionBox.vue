<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>{{questionDetails.question}}</template>

      <hr class="my-4" />

      <p>Some answers here</p>

      <b-button variant="primary" href="#">Do Something</b-button>
      <b-button variant="success" href="#" v-on:click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  name: "QuestionBox",
  props: {
    questionDetails: Object,
    next: Function
  }
};
</script>


<style scoped>
.question-box-container {
  margin: 3%;
  text-align: center;
}
</style>