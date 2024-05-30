<script setup>
import { ref } from 'vue';

const questions = [
  {
    text: 'Which form is correct for "he" in Past Simple?',
    answers: ['he go', 'he went', 'he going', 'he gone'],
    correct: 1,
  },
  {
    text: 'What is the correct negative form for "I played" in Past Simple?',
    answers: ['I did not played', 'I do not play', 'I did not play', 'I not played'],
    correct: 2,
  },
  {
    text: 'How do you form a question in Past Simple for "you worked"?',
    answers: ['Did you work?', 'Do you worked?', 'Did you worked?', 'You did work?'],
    correct: 0,
  },
  {
    text: 'Which verb form should be used with "they" in Past Simple?',
    answers: ['they plays', 'they played', 'they playing', 'they play'],
    correct: 1,
  },
  {
    text: 'What is the correct form for "she" in Past Simple?',
    answers: ['she eat', 'she eats', 'she eating', 'she ate'],
    correct: 3,
  },
  {
    text: 'Which auxiliary verb is used to form questions in Past Simple?',
    answers: ['do', 'be', 'did', 'have'],
    correct: 2,
  },
  {
    text: 'How do you form the negative of "he liked"?',
    answers: ['He did not liked', 'He did not like', 'He does not like', 'He do not like'],
    correct: 1,
  },
  {
    text: 'What is the correct form for "they" in a negative sentence in Past Simple?',
    answers: ['They did not play', 'They do not played', 'They not play', 'They did not played'],
    correct: 0,
  },
  {
    text: 'Which question form is correct for "she worked"?',
    answers: ['Did she worked?', 'Did she work?', 'Do she work?', 'Does she worked?'],
    correct: 1,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['He did not liked coffee', 'He does not like coffee', 'He did not like coffee', 'He do not like coffee'],
    correct: 2,
  },
  {
    text: 'Which form is correct for "we" in Past Simple?',
    answers: ['we go', 'we went', 'we going', 'we gone'],
    correct: 1,
  },
  {
    text: 'How do you form a question for "they played" in Past Simple?',
    answers: ['Did they play?', 'Do they played?', 'Are they played?', 'Did they played?'],
    correct: 0,
  },
  {
    text: 'What is the correct negative form for "she watched"?',
    answers: ['She did not watch', 'She did not watches', 'She do not watch', 'She does not watch'],
    correct: 0,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['I did not played soccer', 'I did not play soccer', 'I do not play soccer', 'I does not played soccer'],
    correct: 1,
  },
  {
    text: 'What is the correct form for "it" in Past Simple?',
    answers: ['it run', 'it runs', 'it running', 'it ran'],
    correct: 3,
  },
  {
    text: 'How do you form a question for "he read" in Past Simple?',
    answers: ['Did he read?', 'Do he read?', 'Is he read?', 'Did he reads?'],
    correct: 0,
  },
  {
    text: 'What is the correct negative form for "we liked"?',
    answers: ['We do not like', 'We did not liked', 'We did not like', 'We do not liked'],
    correct: 2,
  },
  {
    text: 'Which question form is correct for "she sang"?',
    answers: ['Did she sang?', 'Did she sing?', 'Do she sing?', 'Does she sang?'],
    correct: 1,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['They did not liked pizza', 'They does not like pizza', 'They did not like pizza', 'They do not like pizza'],
    correct: 2,
  },
  {
    text: 'What is the correct form for "I" in Past Simple?',
    answers: ['I goes', 'I go', 'I went', 'I gone'],
    correct: 2,
  }
]


const userAnswers = ref(questions.map(() => null));
const showResults = ref(false);
const score = ref(0);

function submitAnswer(questionIndex, answerIndex) {
  userAnswers.value[questionIndex] = answerIndex;
}

function calculateScore() {
  // Вычисляем общий балл
  score.value = questions.reduce((total, question, index) => {
    return total + (userAnswers.value[index] === question.correct ? 1 : 0);
  }, 0);
  
  // Показываем результаты
  showResults.value = true;

  // Вычисляем процент правильных ответов
  const percentage = (score.value / questions.length) * 100;

  // Получаем текущее значение user из localStorage
  let user = JSON.parse(localStorage.getItem('user') || '{}');

  // Добавляем результат теста в объект user
  user['past-simple-test'] = percentage;

  // Сохраняем обновленный объект user обратно в localStorage
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
        <p class="text-xl font-bold mb-4">Сіздің нәтижеңіз:  {{ score }} барлығы {{ questions.length }}</p>
        <ul>
          <li v-for="(question, index) in questions" :key="index" class="mb-3">
            <p class="font-semibold">{{ question.text }}</p>
            <p
              :class="{'text-green-500': userAnswers[index] === question.correct, 'text-red-500': userAnswers[index] !== question.correct}"
            >
              Сіздің жауабыңыз:{{ question.answers[userAnswers[index]] }}
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
