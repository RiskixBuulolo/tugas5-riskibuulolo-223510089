<template>
    <q-page class="q-pa-md">
      <!-- Carousel -->
      <div class="q-gutter-md">
        <q-carousel
          ref="carousel"
          v-model="slide"
          transition-prev="scale"
          transition-next="scale"
          swipeable
          animated
          control-color="white"
          navigation
          padding
          arrows
          height="300px"
          class="bg-primary text-white shadow-1 rounded-borders"
          @mouseenter="stopCarousel"
          @mouseleave="startCarousel"
        >
          <q-carousel-slide name="slide1" class="column no-wrap flex-center">
            <q-img src="../assets/laptop1.jpg" alt="Slide 1" />
            <div class="q-mt-md text-center">
              Slide 1
            </div>
          </q-carousel-slide>
          <q-carousel-slide name="slide2" class="column no-wrap flex-center">
            <q-img src="../assets/laptop2.jpg" alt="Slide 2" />
            <div class="q-mt-md text-center">
              Slide 2
            </div>
          </q-carousel-slide>
          <q-carousel-slide name="slide3" class="column no-wrap flex-center">
            <q-img src="../assets/laptop3.jpg" alt="Slide 3" />
            <div class="q-mt-md text-center">
              Slide 3
            </div>
          </q-carousel-slide>
        </q-carousel>
      </div>
  
      <!-- Laptops -->
      <div class="text-h6 q-mb-md">Laptops</div>
      <div class="q-pa-md q-gutter-md">
        <q-card-group deck>
          <!-- Iterate over laptops array -->
          <q-card v-for="laptop in laptops" :key="laptop.id" class="my-card bg-purple text-white">
            <q-card-section>
              <!-- Display laptop name -->
              <div class="text-h6">{{ laptop.name }}</div>
              <!-- Display laptop price -->
              <div class="text-subtitle2">{{ laptop.price }}</div>
            </q-card-section>
            <q-card-actions>
              <!-- Example action button -->
              <q-btn flat>Beli</q-btn>
            </q-card-actions>
          </q-card>
        </q-card-group>
      </div>
    </q-page>
  </template>
  
  <script>
  export default {
    data() {
      return {
        slide: 0, // Initialize carousel slide index
        intervalId: null,
        laptops: [
          { id: 1, name: 'Laptop ASUS ROG Strix', price: 'Rp 20.000.000' },
          { id: 2, name: 'Laptop Acer Predator', price: 'Rp 18.500.000' },
          { id: 3, name: 'Laptop MacBook Pro', price: 'Rp 35.000.000' },
          { id: 4, name: 'Laptop Lenovo ThinkPad', price: 'Rp 15.000.000' },
          { id: 5, name: 'Laptop HP Spectre x360', price: 'Rp 22.000.000' }
        ]
      };
    },
    mounted() {
      this.startCarousel();
    },
    methods: {
      startCarousel() {
        this.intervalId = setInterval(() => {
          if (this.slide === 2) {
            this.slide = 0; // Set slide back to the first slide
          } else {
            this.$refs.carousel.next(); // Move to the next slide
          }
        }, 1000); // Change 3000 to the desired interval in milliseconds
      },
      stopCarousel() {
        clearInterval(this.intervalId);
      }
    }
  };
  </script>
  
  <style scoped>
  /* Custom styling for product item */
  .product-item {
    margin: 20px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  </style>
  