<script setup>
  import { defineProps } from 'vue';
  import {RouterLink} from 'vue-router';

  const {quizQuestionLength, numberCorrectAnswers} = defineProps(['quizQuestionLength', 'numberCorrectAnswers']);
</script>

<template>
  <div class="results">
    <p>Your result: </p>
    <h2>
      {{ numberCorrectAnswers }} / {{ quizQuestionLength }}
    </h2>
    <RouterLink to="/">To Start Page</RouterLink>
  </div>
</template>

<style scoped>
  .results {
    /*text-align: center;*/
    padding: 100px 0; 
  }
  p {font-size: 25px;}
  h2 {font-size: 60px;}
</style>