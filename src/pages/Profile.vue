<template>
    <div v-if="profileVisible" class="profile-content q-pa-md">
      <div class="profile-header">
        <q-avatar size="150px">
          <img src="../assets/pp.jpg">
        </q-avatar>
        <div class="profile-info q-ml-md">
          <div class="text-h5">{{ userProfile.name }}</div>
          <div class="text-subtitle1">{{ userProfile.company }}</div>
        </div>
      </div>
      <div class="profile-body q-mt-lg">
        <div class="text-h6">Social Media:</div>
        <div class="social-icons q-mt-sm">
          <img src="../assets/fb.jpg" class="social-icon" @click="openSocialMedia(userProfile.facebook)" />&nbsp;
          <img src="../assets/ig.jpg" class="social-icon" @click="openSocialMedia(userProfile.instagram)" />&nbsp;
          <img src="../assets/dc.jpg" class="social-icon" @click="openSocialMedia(userProfile.discord)" />&nbsp;
          <img src="../assets/wechat.png" class="social-icon" @click="openSocialMedia(userProfile.wechat)" />&nbsp;
          <img src="../assets/line.png" class="social-icon" @click="openSocialMedia(userProfile.line)" />&nbsp;
        </div>
      </div>
    </div>
  
    <div v-else-if="salesVisible" class="sales-content q-pa-md">
      <div class="sales-header">
        <q-avatar size="150px">
          <img src="../assets/pp.jpg">
        </q-avatar>
        <div class="sales-info q-ml-md">
          <div class="text-h5">Sales Overview</div>
          <div class="text-subtitle1">Your Sales Performance</div>
        </div>
      </div>
      <div class="sales-body q-mt-lg">
        <div class="text-h6">Sales Data:</div>
        <div class="sales-stats q-mt-sm">
          <p>Total Sales: $10,000</p>
          <p>Monthly Growth: 10%</p>
          <p>Top Products: Laptop A, Laptop B, Accessory C</p>
        </div>
      </div>
    </div>
  
    <div v-else-if="storeRatingsVisible" class="ratings-content q-pa-md">
      <div class="ratings-header">
        <q-avatar size="150px">
          <img src="../assets/pp.jpg">
        </q-avatar>
        <div class="ratings-info q-ml-md">
          <div class="text-h5">Store Ratings</div>
          <div class="text-subtitle1">Customer Feedback</div>
        </div>
      </div>
      <div class="ratings-body q-mt-lg">
        <div class="text-h6">Ratings Data:</div>
        <div class="ratings-stats q-mt-sm">
          <p>Average Rating: 4.5/5</p>
          <p>Total Reviews: 150</p>
          <p>Top Feedback: Great customer service, Fast shipping, Quality products</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      userProfile: Object,
      profileVisible: Boolean,
      salesVisible: Boolean,
      storeRatingsVisible: Boolean,
      openSocialMedia: Function
    }
  }
  </script>
  
  <style scoped>
    .profile-content, .sales-content, .ratings-content {
      max-width: 600px;
      margin: 0 auto;
      text-align: center;
    }
  
    .profile-header, .sales-header, .ratings-header {
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    .profile-info, .sales-info, .ratings-info {
      margin-left: 20px;
    }
  
    .profile-body, .sales-body, .ratings-body {
      margin-top: 20px;
    }
  
    .social-icon {
      width: 50px;
      height: 50px;
      cursor: pointer;
      transition: transform 0.2s;
    }
  
    .social-icon:hover {
      transform: scale(1.2);
    }
  </style>
  