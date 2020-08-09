<template>
  <div id="app">
    <Navbar />
    <b-container class="bv-example-row">
      <b-row sm="6" offset="3">
        <b-col>
          
          <QuestionBox />
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
   
    console.log(result)
    
  }
};
</script>

<style>
</style>
