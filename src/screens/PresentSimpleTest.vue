<script setup>
import { ref } from 'vue';

const questions = [
  {
    text: 'Which form is correct for "he" in Present Simple?',
    answers: ['he go', 'he goes', 'he going', 'he gone'],
    correct: 1,
  },
  {
    text: 'What is the correct negative form for "I play" in Present Simple?',
    answers: ['I does not play', 'I am not play', 'I do not play', 'I not play'],
    correct: 2,
  },
  {
    text: 'How do you form a question in Present Simple for "you work"?',
    answers: ['Are you work?', 'You do work?', 'Do you work?', 'You are work?'],
    correct: 2,
  },
  {
    text: 'Which verb form should be used with "they" in Present Simple?',
    answers: ['they plays', 'they play', 'they playing', 'they played'],
    correct: 1,
  },
  {
    text: 'What is the correct form for "she" in Present Simple?',
    answers: ['she eat', 'she eats', 'she eating', 'she eaten'],
    correct: 1,
  },
  {
    text: 'Which auxiliary verb is used to form questions in Present Simple?',
    answers: ['do', 'be', 'have', 'will'],
    correct: 0,
  },
  {
    text: 'How do you form the negative of "he likes"?',
    answers: ['He does not likes', 'He do not like', 'He does not like', 'He do not likes'],
    correct: 2,
  },
  {
    text: 'What is the correct form for "they" in a negative sentence in Present Simple?',
    answers: ['They does not play', 'They do not play', 'They not play', 'They does not plays'],
    correct: 1,
  },
  {
    text: 'Which question form is correct for "she work"?',
    answers: ['Do she work?', 'Does she works?', 'Does she work?', 'Do she works?'],
    correct: 2,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['He don\'t like coffee', 'He doesn\'t like coffee', 'He not like coffee', 'He isn\'t like coffee'],
    correct: 1,
  },
  {
    text: 'Which form is correct for "we" in Present Simple?',
    answers: ['we goes', 'we going', 'we go', 'we gone'],
    correct: 2,
  },
  {
    text: 'How do you form a question for "they play" in Present Simple?',
    answers: ['Do they play?', 'Does they play?', 'Are they play?', 'Do they playing?'],
    correct: 0,
  },
  {
    text: 'What is the correct negative form for "she watches"?',
    answers: ['She do not watch', 'She does not watches', 'She do not watches', 'She does not watch'],
    correct: 3,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['I doesn\'t play soccer', 'I don\'t plays soccer', 'I don\'t play soccer', 'I do not plays soccer'],
    correct: 2,
  },
  {
    text: 'What is the correct form for "it" in Present Simple?',
    answers: ['it run', 'it runs', 'it running', 'it ran'],
    correct: 1,
  },
  {
    text: 'How do you form a question for "he reads" in Present Simple?',
    answers: ['Does he read?', 'Do he read?', 'Is he read?', 'Does he reads?'],
    correct: 0,
  },
  {
    text: 'What is the correct negative form for "we like"?',
    answers: ['We do not like', 'We does not like', 'We do not likes', 'We does not likes'],
    correct: 0,
  },
  {
    text: 'Which question form is correct for "she sings"?',
    answers: ['Do she sing?', 'Does she sing?', 'Is she sings?', 'Do she sings?'],
    correct: 1,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['They don\'t likes pizza', 'They doesn\'t like pizza', 'They not like pizza', 'They don\'t like pizza'],
    correct: 3,
  },
  {
    text: 'What is the correct form for "I" in Present Simple?',
    answers: ['I goes', 'I go', 'I going', 'I gone'],
    correct: 1,
  }
]


const userAnswers = ref(questions.map(() => null));
const showResults = ref(false);
const score = ref(0);

function submitAnswer(questionIndex, answerIndex) {
  userAnswers.value[questionIndex] = answerIndex;
}

function calculateScore() {
  // Жалпы баллды есептейміз
  score.value = questions.reduce((total, question, index) => {
    return total + (userAnswers.value[index] === question.correct ? 1 : 0);
  }, 0);
  
  // Нәтижелерді көрсетеміз
  showResults.value = true;

  // Дұрыс жауаптардың пайызын есептейміз
  const percentage = (score.value / questions.length) * 100;

  // localStorage-тан қазіргі user мәнін аламыз
  let user = JSON.parse(localStorage.getItem('user') || '{}');

  // user объектіне тест нәтижесін қосамыз
  user['present-simple-test'] = percentage;

  // Жаңартылған user объектісін қайта localStorage-қа сақтаймыз
  localStorage.setItem('user', JSON.stringify(user));
}

</script>

<template>
    <div class="max-w-3xl mx-auto p-6 text-white bg-gray-800 border-4 border-purple-500 shadow-lg">
      <div v-if="!showResults">
        <div v-for="(question, qIndex) in questions" :key="qIndex" class="mb-4">
          <p class="text-lg font-semibold">{{ question.text }}</p>
          <div class="mt-2">
            <button
            v-for="(answer, aIndex) in question.answers"
            :key="aIndex"
            @click="submitAnswer(qIndex, aIndex)"
            :class="[userAnswers[qIndex] === aIndex ? 'bg-blue-600' : 'bg-purple-500', 'hover:bg-purple-700 text-white font-bold py-2 px-4 rounded mr-2 mb-2']"
            >
            {{ answer }}
            </button>
          </div>
        </div>
        <button
          @click="calculateScore"
          class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded"
        >
          Нәтижені көрсету
        </button>
      </div>
  
      <div v-else class="mt-6">
        <p class="text-xl font-bold mb-4">Сіздің нәтижеңіз:  {{ score }} барлығы: {{ questions.length }}</p>
        <ul>
          <li v-for="(question, index) in questions" :key="index" class="mb-3">
            <p class="font-semibold">{{ question.text }}</p>
            <p
              :class="{'text-green-500': userAnswers[index] === question.correct, 'text-red-500': userAnswers[index] !== question.correct}"
            >
              Сіздің жауабыңыз: {{ question.answers[userAnswers[index]] }}
            </p>
            <p class="text-green-500">
              Дұрыс жауап: {{ question.answers[question.correct] }}
            </p>
          </li>
        </ul>
        <button
          @click="() => showResults = false"
          class="bg-purple-500 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded"
        >
          Қайта тапсыру
        </button>
      </div>
    </div>
  </template>
  


<style scoped>
</style>
