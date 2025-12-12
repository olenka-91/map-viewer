<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <!-- Навигация -->
    <nav>
      <RouterLink to="/">Home </RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
  </header>

  <!-- Сюда будут подставляться страницы -->
  <RouterView />
</template>
