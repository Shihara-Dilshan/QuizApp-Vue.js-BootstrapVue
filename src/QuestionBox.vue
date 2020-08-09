<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>Some questions here</template>

      <hr class="my-4" />

      <p>Some answers here</p>

      <b-button variant="primary" href="#">Do Something</b-button>
      <b-button variant="success" href="#">Do Something Else</b-button>
    
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  name: "QuestionBox"
};
</script>


<style scoped>
.question-box-container {
  margin: 3%;
  text-align: center;
}
</style>