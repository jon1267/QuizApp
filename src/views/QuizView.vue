<script setup>
  import Question from '../components/Question.vue';
  import QuizHeader from '../components/QuizHeader.vue';
  import { useRoute } from 'vue-router';
  import { ref } from 'vue';
  import quizes from "../data/quizes.json";

  const route = useRoute();
  const quizId = route.params.id; //console.log(quizId);
  //console.log(quizes);
  
  const quiz = quizes.find(q => q.id == quizId)
  console.log(quiz);
  const currentQuestionIndex = ref(0);

</script>

<template>
  <div>
      <QuizHeader />
    <div>
      <Question :question="quiz.questions[currentQuestionIndex]" />
    </div>
  </div>
</template>