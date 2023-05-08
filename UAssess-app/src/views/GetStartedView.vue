<template>
    <div class="get-started-page">
      <div class="get-started-body">
        <div class="desc"><h2>Welcome to UAssess!</h2></div>
        <div class="btns">
          <div class="btn-1">
            <router-link to="/jhs-admission-test" class="dept-btn">JUNIOR HIGH SCHOOL</router-link>
          </div>
          <div class="btn-2">
            <router-link to="/shs-admission-test" class="dept-btn">SENIOR HIGH SCHOOL</router-link>
          </div>
          <div class="btn-3">
            <router-link to="/college-admission-test" class="dept-btn">COLLEGE</router-link>
          </div>
        </div>
      </div>
    </div>
    </template>
    
    <script setup>
    import '../assets/get-started.css'
    import { createRouter, createWebHistory } from 'vue-router'
    
    const router = createRouter({
      history: createWebHistory(),
      routes: [
        {
          path: '/jhs-admission-test',
          name: 'JHSAdmissionTest',
          component: () => import('../views/JhsView.vue')
        },
        {
          path: '/shs-admission-test',
          name: 'SHSAdmissionTest',
          component: () => import('../views/ShsView.vue')
        },
        {
          path: '/college-admission-test',
          name: 'CollegeAdmissionTest',
          component: () => import('../views/CollegeView.vue')
        },
      ],
    })
    </script>