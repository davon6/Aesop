<template>
<div class="question-box-container">
  <b-jumbotron>
    <template slot="lead">
        {{ currentQuestion.question}}
      </template>

      <hr class="my-4">

      <p v-for="(answer, index) in answers" :key="index">
     {{answer}}
      </p>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
</div>
</template>

<script>
export default {
  props: {
    currentQuestion: Object,
    next: Function
  },
  computed: {
    answers(){
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
         return answers
    }
  },
  mounted(){
    console.log(this.currentQuestion)
  }
}
</script>