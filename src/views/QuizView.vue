<script setup>
  import Question from '../components/Question.vue';
  import QuizHeader from '../components/QuizHeader.vue';
  import Result from '../components/Result.vue';
  import { useRoute } from 'vue-router';
  import { ref, watch, computed } from 'vue';
  import quizes from "../data/quizes.json";
  //console.log(quizes);

  const route = useRoute();
  const quizId = route.params.id; //console.log(quizId);
  const quiz = quizes.find(q => q.id == quizId); //console.log(quiz); 
  const currentQuestionIndex = ref(0);
  const numberCorrectAnswers = ref(0);
  const showResults = ref(false);

  // const && watch work together
  //const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)
  //watch(
  //  () => currentQuestionIndex.value, 
  //  () => {questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`}
  //);

  const questionStatus = computed(() => {
    return `${currentQuestionIndex.value}/${quiz.questions.length}`  
  });
  const barPercentage = computed(() => {
    return `${currentQuestionIndex.value/quiz.questions.length * 100}%`
  });

  const onOptionSelected = (isCorrect) => {
    if(isCorrect) {
      numberCorrectAnswers.value++;
    }

    if(quiz.questions.length - 1 === currentQuestionIndex.value) {
      showResults.value = true
    }
    currentQuestionIndex.value++;
  }
</script>

<template>
  <div>
    {{ barPercentage }}
      <QuizHeader 
        :questionStatus = "questionStatus"
        :barPercentage = "barPercentage" 
      />
    <div>
      <Question 
        v-if="!showResults"
        :question="quiz.questions[currentQuestionIndex]" 
        @selectOption="onOptionSelected"
      />
      <Result 
        v-else 
        :quizQuestionLength="quiz.questions.length"
        :numberCorrectAnswers="numberCorrectAnswers"
      />
    </div>
    <!-- <button @click="currentQuestionIndex++">Next Question</button> -->
    <!-- -- <button @click="currentQuestionIndex--">Back Previus</button> -- -->
  </div>
</template>