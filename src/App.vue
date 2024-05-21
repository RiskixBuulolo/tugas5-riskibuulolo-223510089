<template>
  <q-layout view="hHh lpR fFf">
    <!-- Header -->
    <q-header elevated class="bg-primary text-white" height-hint="98">
      <!-- Toolbar -->
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
        <!-- Title -->
        <q-toolbar-title>
          <q-avatar>
            <img src="./assets/icon.svg">
          </q-avatar>
          Laptop Store
        </q-toolbar-title>
        <!-- Cart Button -->
        <q-btn dense flat round icon="cart" @click="openCart" />
        <!-- Profile Button -->
        <q-btn dense flat round icon="account_circle" @click="toggleRightDrawer"/>
      </q-toolbar>
      <!-- Tabs -->
      <q-tabs align="left" v-model="currentTab">
        <q-tab name="laptops" label="Laptops" />
        <q-tab name="accessories" label="Accessories" />
        <q-tab name="about" label="About Us" />
      </q-tabs>
    </q-header>

    <!-- Left Drawer -->
    <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
      <q-list>
        <q-item clickable v-ripple @click="navigateTo('laptops')">
          <q-item-section>
            <q-item-label>Laptops</q-item-label>
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple @click="navigateTo('accessories')">
          <q-item-section>
            <q-item-label>Accessories</q-item-label>
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple @click="navigateTo('about')">
          <q-item-section>
            <q-item-label>About Us</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!-- Right Drawer -->
    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <div class="q-pa-md">
        <div class="text-center">
          <q-avatar size="100px">
            <img src="./assets/pp.jpg">
          </q-avatar>
          <div class="text-h6 q-mt-md">{{ userProfile.name }}</div>
          <div class="text-caption">{{ userProfile.company }}</div>
          <div class="q-mt-md">
            <img src="./assets/fb.jpg" class="social-icon" @click="openSocialMedia(userProfile.facebook)" />&nbsp;
          <img src="./assets/ig.jpg" class="social-icon" @click="openSocialMedia(userProfile.instagram)" />&nbsp;
          <img src="./assets/dc.jpg" class="social-icon" @click="openSocialMedia(userProfile.discord)" />&nbsp;
          <img src="./assets/wechat.png" class="social-icon" @click="openSocialMedia(userProfile.wechat)" />&nbsp;
          <img src="./assets/line.png" class="social-icon" @click="openSocialMedia(userProfile.line)" />&nbsp;
          </div>
        </div>
        <q-list bordered class="q-mt-md">
          <q-item clickable v-ripple @click="editProfile">
            <q-item-section>
              <q-item-label>Profile</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable v-ripple @click="goToSales">
            <q-item-section>
              <q-item-label>Sales</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable v-ripple @click="goToStoreRatings">
            <q-item-section>
              <q-item-label>Store Ratings</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </div>
    </q-drawer>

    <!-- Page Content -->
    <q-page-container>
      <component :is="currentComponent" v-if="!profileVisible && !salesVisible && !storeRatingsVisible" />
      <Profile v-else
               :userProfile="userProfile"
               :profileVisible="profileVisible"
               :salesVisible="salesVisible"
               :storeRatingsVisible="storeRatingsVisible"
               :openSocialMedia="openSocialMedia" />
    </q-page-container>

    <!-- Footer -->
    <q-footer elevated class="bg-grey-8 text-white" style="height: 65px">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="./assets/icon.svg">
          </q-avatar>
          <div>Laptop Store &copy; 2024</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { ref, computed } from 'vue'
import Laptops from './pages/Laptops.vue'
import Accessories from './pages/Accessories.vue'
import About from './pages/About.vue'
import Profile from './pages/Profile.vue'

export default {
  components: {
    Laptops,
    Accessories,
    About,
    Profile
  },
  setup () {
    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(false)
    const currentTab = ref('laptops')
    const userProfile = ref({
      name: 'Riski Buulolo',
      company: 'PT Risester',
      facebook: 'https://facebook.com',
      twitter: 'https://twitter.com',
      linkedin: 'https://linkedin.com'
    })
    const profileVisible = ref(false)
    const salesVisible = ref(false)
    const storeRatingsVisible = ref(false)

    const openCart = () => {
      alert('Cart opened')
    }

    const navigateTo = (tab) => {
      currentTab.value = tab
      profileVisible.value = false
      salesVisible.value = false
      storeRatingsVisible.value = false
    }

    const currentComponent = computed(() => {
      switch (currentTab.value) {
        case 'laptops':
          return Laptops
        case 'accessories':
          return Accessories
        case 'about':
          return About
        default:
          return Laptops
      }
    })

    const toggleLeftDrawer = () => {
      leftDrawerOpen.value = !leftDrawerOpen.value
    }

    const toggleRightDrawer = () => {
      rightDrawerOpen.value = !rightDrawerOpen.value
    }

    const editProfile = () => {
      profileVisible.value = true
      salesVisible.value = false
      storeRatingsVisible.value = false
    }

    const goToSales = () => {
      salesVisible.value = true
      profileVisible.value = false
      storeRatingsVisible.value = false
    }

    const goToStoreRatings = () => {
      storeRatingsVisible.value = true
      profileVisible.value = false
      salesVisible.value = false
    }

    const openSocialMedia = (url) => {
      window.open(url, '_blank')
    }

    return {
      leftDrawerOpen,
      toggleLeftDrawer,
      rightDrawerOpen,
      toggleRightDrawer,
      openCart,
      navigateTo,
      currentTab,
      currentComponent,
      userProfile,
      profileVisible,
      salesVisible,
      storeRatingsVisible,
      editProfile,
      goToSales,
      goToStoreRatings,
      openSocialMedia
    }
  }
}
</script>

<style>
  .product-item {
    margin: 20px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  .my-card {
    margin: 20px;
    padding: 20px;
    border-radius: 5px;
  }

  .social-icon {
      width: 40px;
      height: 40px;
      cursor: pointer;
      transition: transform 0.2s;
    }
  
    .social-icon:hover {
      transform: scale(1.2);
    }
</style>
