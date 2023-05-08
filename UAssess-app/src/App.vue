<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <!--
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/vue-js-easy-quiz">Easy</RouterLink>
        <RouterLink to="/vue-js-moderate-quiz">Moderate</RouterLink>
        <RouterLink to="/vue-js-hard-quiz">Hard</RouterLink>
      </nav>

  <RouterView />

    -->
    <RouterLink to="/"></RouterLink>
    <RouterLink to="/get-started"></RouterLink>
    <RouterLink to="/jhs-admission-test"></RouterLink>
<RouterView />
</template>