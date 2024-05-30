<template>
  <div class="flex flex-wrap justify-center">
    <a href="https://www.superteacherworksheets.com/reading-comp/6th-elephant-seals_SNOUT.pdf" class="card-link">
      <div class="card">
        <h1 class="card-title">Elephant Seals</h1>  
        <p class="card-description">The world's largest seals make their home in the frigid Antarctic. Learn all about elephant seals and how they've adapted to their environment. 6th Grade</p>
      </div>
    </a>

    <a href="https://www.superteacherworksheets.com/reading-comp/6th-red-kangaroo_KANGA.pdf" class="card-link">
      <div class="card">
        <h1 class="card-title">World's Largest Marsupial</h1>  
        <p class="card-description">This article will teach students about the red kangaroo. Measuring 6 feet tall and weighing 200 pounds, it is the world's largest marsupial. 6th Grade</p>
      </div>
    </a>

    <a href="https://www.superteacherworksheets.com/reading-comp/6th-falling-asleep_SLEEP.pdf" class="card-link">
      <div class="card">
        <h1 class="card-title">Falling Asleep</h1>  
        <p class="card-description">The person in this poem is worrying about the shadows on the walls and can not fall asleep. 6th Grade</p>
      </div>
    </a>

    <a href="https://www.superteacherworksheets.com/reading-comp/science-innerplanets_WBRRN.pdf" class="card-link">
      <div class="card">
        <h1 class="card-title">The Inner Planets</h1>  
        <p class="card-description">Learn about the terrestrial inner planets of our solar system. <br> 5th through 7th Grades</p>
      </div>
    </a>
  </div>
</template>

<style scoped>
.card-link {
  flex: 0 0 33.33333%;
  max-width: 33.33333%;
  padding: 10px;
}

.card {
  background-color: #8B5CF6;
  color: white;
  border-radius: 5px;
  transition: background-color 0.3s ease;
  width: 100%;
  height: 150px;
}

.card:hover {
  background-color: #6D28D9;
}

.card-title {
  font-size: 24px;
}

.card-description {
  font-size: 18px;
  margin-top: 10px;
}
</style>
