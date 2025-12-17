<script setup lang="ts">
import { RouterView } from 'vue-router'
import { ref, onMounted } from 'vue'

// Для примера: отслеживаем размер окна
const windowWidth = ref(window.innerWidth)

onMounted(() => {
  window.addEventListener('resize', () => {
    windowWidth.value = window.innerWidth
  })
})

const updateWindowWidth = () => {
  windowWidth.value = window.innerWidth
}
</script>

<template>
  <!-- Основной контейнер на весь экран -->
  <div class="min-h-screen bg-gradient-to-br from-gray-50 to-gray-100">
    <!-- Header / Шапка приложения -->
    <header class="bg-white/80 backdrop-blur-sm border-b border-gray-200 sticky top-0 z-50">
      <div class="container mx-auto px-4 py-3">
        <div class="flex items-center justify-between">
          <!-- Логотип и название -->
          <div class="flex items-center space-x-3">
            <div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center">
              <span class="text-white font-bold">M</span>
            </div>
            <div>
              <h1 class="text-xl font-bold text-gray-800">Map Viewer</h1>
              <p class="text-sm text-gray-500">Визуализация геоданных и маршрутов</p>
            </div>
          </div>

          <!-- Навигация -->
          <nav class="flex items-center space-x-1">
            <button class="btn-secondary text-sm">
              <svg class="w-5 h-5 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                  d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
              Настройки
            </button>

            <button class="btn-primary text-sm">
              <svg class="w-5 h-5 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
              </svg>
              Новая точка
            </button>
          </nav>
        </div>
      </div>
    </header>

    <!-- Основное содержимое -->
    <main class="container mx-auto px-4 py-6">
      <!-- Здесь будут отображаться страницы (карта, настройки и т.д.) -->
      <RouterView />
    </main>

    <!-- Footer / Подвал -->
    <footer class="bg-white/60 border-t border-gray-200 mt-8">
      <div class="container mx-auto px-4 py-4">
        <div class="flex flex-col md:flex-row justify-between items-center text-sm text-gray-600">
          <div class="mb-2 md:mb-0">
            <span class="font-medium">Map Viewer v1.0</span>
            <span class="mx-2">•</span>
            <span>Разработано с использованием Vue 3, Go и PostgreSQL</span>
          </div>
          <div>
            Размер окна: {{ windowWidth }}px
            <span class="mx-2">•</span>
            <button @click="updateWindowWidth" class="text-blue-600 hover:text-blue-800">
              Обновить
            </button>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
/* Локальные стили для этого компонента */
header {
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}

footer {
  backdrop-filter: blur(10px);
}
</style>
