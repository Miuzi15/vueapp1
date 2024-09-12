<template>
  <div id="app" :style="{ backgroundColor: currentColor }" @click="incrementCount">
    <h1>Vue Single Page App</h1>

    <!-- 1. Click Counter -->
    <div class="counter">
      <h2>Click Counter</h2>
      <p> {{ count }} </p>
      <button @click.stop="undoCount" :disabled="countHistory.length === 0">Undo</button>
    </div>

    <!-- 2. Box Color Changer -->
    <div class="color-changer">
      <h2>Box Color Changer</h2>
      <button @click.stop="changeColor">Change Color</button>
    </div>

    <!-- 3. Image Carousel -->
    <div class="carousel">
      <h2>Image Carousel</h2>
      <div class="carousel-container">
        <img :src="images[currentImageIndex]" :alt="'Image ' + (currentImageIndex + 1)" class="carousel-image" />
      </div>
      <button @click.stop="prevImage">Previous</button>
      <button @click.stop="nextImage">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0, // Counter
      countHistory: [], // To store the history of clicks for undo
      colors: ['pink', 'blue', 'green', 'yellow'], // Color Changer
      currentColor: 'pink',
      images: [
        // Image Carousel
        'https://i.pinimg.com/564x/8d/bb/38/8dbb38193796d1ff708a75691c913fcb.jpg',
        'https://i.pinimg.com/736x/1c/02/52/1c0252c271311e22a733519e89126ce8.jpg',
        'https://i.pinimg.com/736x/97/31/3a/97313a30e351a86f099fa636ca9a4685.jpg',
      ],
      currentImageIndex: 0,
    };
  },
  methods: {
    incrementCount() {
      // Save current count to history before incrementing
      this.countHistory.push(this.count);
      this.count++;
    },
    undoCount() {
      // Restore the previous count from history
      if (this.countHistory.length > 0) {
        this.count = this.countHistory.pop();
      }
    },
    changeColor() {
      const randomIndex = Math.floor(Math.random() * this.colors.length);
      this.currentColor = this.colors[randomIndex];
    },
    nextImage() {
      this.currentImageIndex = (this.currentImageIndex + 1) % this.images.length;
    },
    prevImage() {
      this.currentImageIndex = (this.currentImageIndex - 1 + this.images.length) % this.images.length;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  height: 100vh; /* Full-screen height */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  transition: background-color 0.5s ease; /* Smooth transition */
  margin: 20px; /* Margin added to all sides */
  padding: 40px; /* Padding added */
}

.counter,
.color-changer,
.carousel {
  margin: 5px 0; /* Margin for individual sections */
  padding: 20px; /* Padding for individual sections */
  border: 1px solid #ddd; /* Optional: Add border for better visual separation */
  border-radius: 10px; /* Optional: Rounded corners */
}

.carousel-container {
  margin: 10px 0;
}

.carousel-image {
  width: 300px;
  height: 200px;
  object-fit: cover;
}
</style>


