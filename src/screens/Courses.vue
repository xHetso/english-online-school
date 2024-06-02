<script>
export default {
  mounted() {
    const images = document.querySelectorAll('img');
    images.forEach(image => {
      image.addEventListener('click', this.openFullscreen);
    });
  },
  methods: {
    openFullscreen(event) {
      const elem = event.target;
      if (elem.requestFullscreen) {
        elem.requestFullscreen();
      } else if (elem.mozRequestFullScreen) { // Firefox
        elem.mozRequestFullScreen();
      } else if (elem.webkitRequestFullscreen) { // Chrome, Safari and Opera
        elem.webkitRequestFullscreen();
      } else if (elem.msRequestFullscreen) { // IE/Edge
        elem.msRequestFullscreen();
      }
    }
  }
}
</script>
<template>
  <div class="grid grid-cols-4 gap-10">
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book1.jpg" alt="Book 1" id="book1">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book2.jpg" alt="Book 2" id="book2">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book3.jpg" alt="Book 3" id="book3">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book4.jpg" alt="Book 4" id="book4">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book5.jpg" alt="Book 5" id="book5">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book6.jpg" alt="Book 6" id="book6">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book7.jpg" alt="Book 7" id="book7">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book8.jpg" alt="Book 8" id="book8">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book9.jpg" alt="Book 9" id="book9">
    </div>
    <div>
      <img class="w-full cursor-pointer" src="/src/assets/images/book10.jpg" alt="Book 10" id="book10">
    </div>
  </div>
</template>

<style scoped>
</style>
