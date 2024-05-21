<template>
    <q-page class="q-pa-md">
      <!-- Carousel -->
      <div class="q-gutter-md">
        <q-carousel
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
          ref="carousel"
        >
          <q-carousel-slide name="slide1" class="column no-wrap flex-center">
            <q-img src="../assets/akses1.jpg" alt="Slide 1" />
            <div class="q-mt-md text-center">
              Slide 1
            </div>
          </q-carousel-slide>
          <q-carousel-slide name="slide2" class="column no-wrap flex-center">
            <q-img src="../assets/akses2.jpg" alt="Slide 2" />
            <div class="q-mt-md text-center">
              Slide 2
            </div>
          </q-carousel-slide>
          <q-carousel-slide name="slide3" class="column no-wrap flex-center">
            <q-img src="../assets/akses3.jpg" alt="Slide 3" />
            <div class="q-mt-md text-center">
              Slide 3
            </div>
          </q-carousel-slide>
        </q-carousel>
      </div>
  
      <!-- Accessories -->
      <div class="text-h6 q-mb-md">Accessories</div>
      <div class="q-pa-md q-gutter-md">
        <q-card-group deck>
          <!-- Iterate over accessories array -->
          <q-card v-for="accessory in accessories" :key="accessory.id" class="my-card bg-green text-white">
            <q-card-section>
              <!-- Display accessory name -->
              <div class="text-h6">{{ accessory.name }}</div>
              <!-- Display accessory price -->
              <div class="text-subtitle2">{{ accessory.price }}</div>
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
        accessories: [
          { id: 1, name: 'Mouse Logitech G502', price: 'Rp 750.000' },
          { id: 2, name: 'Keyboard Mechanical Razer', price: 'Rp 1.500.000' },
          { id: 3, name: 'Headset Gaming HyperX', price: 'Rp 1.200.000' },
          { id: 4, name: 'Cooling Pad Cooler Master', price: 'Rp 350.000' },
          { id: 5, name: 'External SSD Samsung T7', price: 'Rp 2.000.000' }
        ]
      };
    },
    mounted() {
      this.startCarousel();
    },
    methods: {
      startCarousel() {
        if (!this.$refs.carousel) return; // Check if the carousel ref exists
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
  