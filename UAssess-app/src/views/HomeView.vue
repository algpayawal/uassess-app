<template>
  <div class="home-page">
    <div class="home-body">
        <div class="left"><img src='../assets/images/head.png' style="width: 1200px;"></div>
        <div class="right">
        <h3>How can I help you today?</h3><br>
        <router-link class="get-started" to="/get-started"> GET STARTED </router-link>
        </div>
    </div>
  </div>
  

</template>

<script setup>
import '../assets/home.css'
import { createRouter, createWebHistory } from 'vue-router'


const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/get-started',
      name: 'GetStarted',
       component: () => import('../views/GetStartedView.vue')
    },
  ],
})

const handleGetStarted = () => {
  router.push('/get-started')
}
</script>

<style>
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Montserrat', sans-serif;
  }
.home-page{
  background-image: url(../assets/images/home-bg.png);
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
}
.home-body {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  grid-auto-columns: 1fr;
  gap: 0px 0px;
  grid-auto-flow: row;
  grid-template-areas:
    "left right";
}

.left {
  grid-area: left;
  margin-top: 320px;
}

.right {
  grid-area: right;
  text-align: right;
  margin-top: 700px;
  margin-right: 140px;
  margin-bottom: 238px;
}

.get-started {
  background-color: #CB2028;
  text-decoration: none;
  color: white;
  font-size: 25px;
  font-weight: bold;
  padding: 25px 50px;
  border: none;
  border-radius: 50px;
  cursor: pointer;
}
</style>