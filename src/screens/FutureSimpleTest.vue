<script setup>
import { ref } from 'vue';

const questions = [
  {
    text: 'Which form is correct for "he" in Future Simple?',
    answers: ['he will go', 'he will goes', 'he will going', 'he will gone'],
    correct: 0,
  },
  {
    text: 'What is the correct negative form for "I will play" in Future Simple?',
    answers: ['I will not plays', 'I will do not play', 'I will not play', 'I will not playing'],
    correct: 2,
  },
  {
    text: 'How do you form a question in Future Simple for "you will work"?',
    answers: ['Will you work?', 'Do you will work?', 'Will you works?', 'You will work?'],
    correct: 0,
  },
  {
    text: 'Which verb form should be used with "they" in Future Simple?',
    answers: ['they will plays', 'they will play', 'they will playing', 'they will played'],
    correct: 1,
  },
  {
    text: 'What is the correct form for "she" in Future Simple?',
    answers: ['she will eat', 'she will eats', 'she will eating', 'she will eaten'],
    correct: 0,
  },
  {
    text: 'Which auxiliary verb is used to form questions in Future Simple?',
    answers: ['do', 'be', 'will', 'have'],
    correct: 2,
  },
  {
    text: 'How do you form the negative of "he will like"?',
    answers: ['He will not likes', 'He will not like', 'He will do not like', 'He will does not like'],
    correct: 1,
  },
  {
    text: 'What is the correct form for "they" in a negative sentence in Future Simple?',
    answers: ['They will not play', 'They will do not played', 'They will not playing', 'They will does not play'],
    correct: 0,
  },
  {
    text: 'Which question form is correct for "she will work"?',
    answers: ['Will she worked?', 'Will she works?', 'Will she work?', 'Do she will work?'],
    correct: 2,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['He will not likes coffee', 'He will does not like coffee', 'He will not like coffee', 'He will do not like coffee'],
    correct: 2,
  },
  {
    text: 'Which form is correct for "we" in Future Simple?',
    answers: ['we will goes', 'we will going', 'we will go', 'we will gone'],
    correct: 2,
  },
  {
    text: 'How do you form a question for "they will play" in Future Simple?',
    answers: ['Will they play?', 'Do they will play?', 'Are they will play?', 'Will they playing?'],
    correct: 0,
  },
  {
    text: 'What is the correct negative form for "she will watch"?',
    answers: ['She will not watch', 'She will not watches', 'She will do not watch', 'She will does not watch'],
    correct: 0,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['I will not plays soccer', 'I will not play soccer', 'I will do not play soccer', 'I will does not played soccer'],
    correct: 1,
  },
  {
    text: 'What is the correct form for "it" in Future Simple?',
    answers: ['it will run', 'it will runs', 'it will running', 'it will ran'],
    correct: 0,
  },
  {
    text: 'How do you form a question for "he will read" in Future Simple?',
    answers: ['Will he read?', 'Do he will read?', 'Is he will read?', 'Will he reads?'],
    correct: 0,
  },
  {
    text: 'What is the correct negative form for "we will like"?',
    answers: ['We will not like', 'We will do not like', 'We will not likes', 'We will does not like'],
    correct: 0,
  },
  {
    text: 'Which question form is correct for "she will sing"?',
    answers: ['Will she sing?', 'Will she sings?', 'Do she will sing?', 'Does she will sing?'],
    correct: 0,
  },
  {
    text: 'Which sentence is correct?',
    answers: ['They will not likes pizza', 'They will does not like pizza', 'They will not like pizza', 'They will do not like pizza'],
    correct: 2,
  },
  {
    text: 'What is the correct form for "I" in Future Simple?',
    answers: ['I will goes', 'I will go', 'I will going', 'I will gone'],
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
  user['future-simple-test'] = percentage;

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
        <p class="text-xl font-bold mb-4">Сіздің нәтижеңіз: {{ score }} барлығы {{ questions.length }}</p>
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
