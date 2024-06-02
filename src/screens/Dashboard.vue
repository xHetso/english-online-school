<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/swiper-bundle.css';

const authors = ref([]);
const comments = ref([
  { id: 1, name: "Анна", comment: "Үздік курстар, көп нәрсені үйрендім!", photo: "./../../src/assets/images/comment1.jpg" },
  { id: 2, name: "Наташа", comment: "Рахмет, сіздің оқыту әдісіңіз ерекше.", photo: "./../../src/assets/images/comment2.jpg" },
  { id: 3, name: "Елена", comment: "Бағдарламалауды бастағысы келетіндерге кеңес беремін.", photo: "./../../src/assets/images/comment3.jpg" },
  { id: 4, name: "Мария", comment: "Тамаша оқытушылар және сапалы материалдар!", photo: "./../../src/assets/images/comment4.jpg" },
  { id: 5, name: "Карина", comment: "Жаңа білімдер мен қызықты әдіс үшін алғыс айтамын!", photo: "./../../src/assets/images/comment5.jpg" }
]);
const router = useRouter();

onMounted(async () => {
  try {
    const response = await axios.get('https://backend-english-school.onrender.com/api/authors');
    authors.value = response.data;
  } catch (error) {
    console.error('Авторларды алу кезінде қате пайда болды:', error);
  }
});

function goToCourses() {
  router.push({ name: 'Сабақтар' }); 
}
</script>

<template>
<div class="flex flex-col justify-center items-center p-10 bg-gradient-to-r from-indigo-700 via-purple-700 to-pink-700 rounded-3xl">
  <h1 class="text-3xl mb-2">Ағылшын тілін оқу арқылы тілді меңгеру!</h1>
  <div class="max-w-4xl mx-auto p-10">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <div @click="goToCourses" class="card bg-gradient-to-tr from-gray-700 to-gray-800 rounded-lg shadow-lg p-6">
        <h3 class="text-xl text-indigo-500 font-semibold mb-4">Түрлі мәтіндер мен әдеби шығармаларды қызықты оқу арқылы ағылшын тілі әлеміне еніңіз.</h3>
        <p>
          Ағылшын тілінің өзіне арналған қосымша тексттер мен әдебиеттің өзінен көз жеткізіңіз.
        </p>
      </div>
      <div @click="goToCourses" class="card bg-gradient-to-tr from-gray-700 to-gray-800 rounded-lg shadow-lg p-6">
        <h3 class="text-xl text-indigo-500 font-semibold mb-4">Материалдардың бейнелері</h3>
        <p>
          Біздің сайтымызда әр оқушының қызығушылығына сәйкес әртүрлі тақырыптардағы мәтіндердің кең ауқымы ұсынылады.
        </p>
      </div>
      <div @click="goToCourses" class="card bg-gradient-to-tr from-gray-700 to-gray-800 rounded-lg shadow-lg p-6">
        <h3 class="text-xl text-indigo-500 font-semibold mb-4">Сіздің деңгейіңізге бағытталған оқу процесі</h3>
        <p>
          Ағылшын тілінің деңгейіне қарамастан, біздің сайт оқу және түсіну дағдыларыңызды дамытуға көмектеседі.
        </p>
      </div>
      <div @click="goToCourses" class="card bg-gradient-to-tr from-gray-700 to-gray-800 rounded-lg shadow-lg p-6">
        <h3 class="text-xl text-indigo-500 font-semibold mb-4">Жаңа әлем ашу үшін оқу</h3>
        <p>
          Әрбір жаңа сөз бен сөз тіркесімен сіз мәдениет пен шекарасыз қарым-қатынасқа еніп, мүмкіндіктеріңізді кеңейтесіз.
        </p>
      </div>
    </div>
  </div>
</div>

</template>

<style scoped>
.card {
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
}
</style>
