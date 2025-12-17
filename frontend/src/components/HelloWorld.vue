<!-- HelloWorld.vue -->
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>Это пример компонента Vue 3.</p>
  </div>
  <div class="bg-green-500 text-white p-4">
    PostCSS + Tailwind работают!
  </div>
</template>


<script setup lang="ts">
// Получаем пропс msg из родителя
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<style scoped>
.hello {
  text-align: center;
  margin: 20px;
  padding: 20px;
  border: 1px solid #ad6363;
  border-radius: 8px;
  background-color: #f9f9f9;
}

h1 {
  color: #44ac7d;
}
</style>
