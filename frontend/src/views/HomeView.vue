<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

// Состояние для демонстрации
const isMapLoaded = ref(false)
const mapScale = ref(1)

// Имитация загрузки карты
onMounted(() => {
  setTimeout(() => {
    isMapLoaded.value = true
  }, 1000)
})

// Функции для демонстрации
const zoomIn = () => {
  if (mapScale.value < 3) mapScale.value += 0.1
}

const zoomOut = () => {
  if (mapScale.value > 0.5) mapScale.value -= 0.1
}

const resetZoom = () => {
  mapScale.value = 1
}
</script>

<template>
  <div class="flex flex-col h-full">
    <!-- Панель управления картой -->
    <div class="bg-white rounded-xl shadow-sm p-4 mb-6">
      <div class="flex flex-wrap items-center justify-between gap-4">
        <!-- Левая часть: элементы управления -->
        <div class="flex items-center space-x-4">
          <div class="flex items-center space-x-2">
            <button @click="zoomOut"
              class="w-10 h-10 rounded-lg bg-gray-100 hover:bg-gray-200 flex items-center justify-center transition-colors"
              title="Уменьшить">
              <svg class="w-5 h-5 text-gray-700" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 12H4" />
              </svg>
            </button>

            <div class="text-center min-w-[60px]">
              <div class="text-lg font-bold text-blue-600">{{ (mapScale * 100).toFixed(0) }}%</div>
              <div class="text-xs text-gray-500">Масштаб</div>
            </div>

            <button @click="zoomIn"
              class="w-10 h-10 rounded-lg bg-gray-100 hover:bg-gray-200 flex items-center justify-center transition-colors"
              title="Увеличить">
              <svg class="w-5 h-5 text-gray-700" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
              </svg>
            </button>

            <button @click="resetZoom" class="btn-secondary text-sm">
              Сбросить
            </button>
          </div>

          <div class="h-8 w-px bg-gray-300"></div>

          <div class="flex items-center space-x-2">
            <button class="btn-secondary text-sm">Точки</button>
            <button class="btn-secondary text-sm">Линии</button>
            <button class="btn-secondary text-sm">Маршруты</button>
          </div>
        </div>

        <!-- Правая часть: информация -->
        <div class="flex items-center space-x-4 text-sm">
          <div class="flex items-center">
            <div class="w-3 h-3 rounded-full bg-green-500 mr-2"></div>
            <span class="text-gray-600">Загружено: </span>
            <span class="font-medium ml-1">{{ isMapLoaded ? '100%' : 'Загрузка...' }}</span>
          </div>

          <div class="hidden md:block">
            <span class="text-gray-600">Координаты: </span>
            <span class="font-mono font-medium">51.5074° N, 0.1278° W</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Основной контейнер для карты -->
    <div class="flex-1 flex flex-col md:flex-row gap-6">
      <!-- Левая панель: Список точек/маршрутов -->
      <div class="md:w-80 bg-white rounded-xl shadow-sm p-4 order-2 md:order-1">
        <h2 class="text-lg font-bold text-gray-800 mb-4">Список объектов</h2>

        <!-- Заглушка для списка -->
        <div class="space-y-3">
          <div v-for="n in 5" :key="n"
            class="p-3 rounded-lg border border-gray-200 hover:border-blue-300 transition-colors">
            <div class="flex justify-between items-start">
              <div>
                <h3 class="font-medium text-gray-800">Точка {{ n }}</h3>
                <p class="text-sm text-gray-500 mt-1">Координаты: {{ n * 10 }}, {{ n * 15 }}</p>
              </div>
              <div class="w-6 h-6 rounded-full"
                :class="n % 3 === 0 ? 'bg-red-500' : n % 3 === 1 ? 'bg-blue-500' : 'bg-green-500'"></div>
            </div>
          </div>
        </div>

        <!-- Подсказка -->
        <div class="mt-6 p-3 bg-blue-50 rounded-lg border border-blue-200">
          <p class="text-sm text-blue-800">
            <span class="font-medium">Совет:</span> Кликните на карте, чтобы добавить новую точку. Выделите две точки для
            построения маршрута.
          </p>
        </div>
      </div>

      <!-- Основная область: Карта -->
      <div class="flex-1 order-1 md:order-2">
        <div class="bg-white rounded-xl shadow-sm overflow-hidden h-full">
          <!-- Контейнер карты с фиксированными пропорциями -->
          <div class="relative h-full min-h-[500px] bg-gray-100">
            <!-- Индикатор загрузки -->
            <div v-if="!isMapLoaded" class="absolute inset-0 flex items-center justify-center bg-gray-100/80 z-10">
              <div class="text-center">
                <div class="w-16 h-16 border-4 border-blue-200 border-t-blue-600 rounded-full animate-spin mx-auto"></div>
                <p class="mt-4 text-gray-600 font-medium">Загрузка карты...</p>
              </div>
            </div>

            <!-- Заглушка карты (пока без изображения) -->
            <div class="absolute inset-0 flex items-center justify-center">
              <div class="text-center max-w-md p-8">
                <!-- Иконка карты -->
                <div class="w-20 h-20 mx-auto mb-6 text-gray-400">
                  <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                      d="M9 20l-5.447-2.724A1 1 0 013 16.382V5.618a1 1 0 011.447-.894L9 7m0 13l6-3m-6 3V7m6 10l4.553 2.276A1 1 0 0021 18.382V7.618a1 1 0 00-.553-.894L15 4m0 13V4m0 0L9 7" />
                  </svg>
                </div>

                <h3 class="text-2xl font-bold text-gray-700 mb-3">Картографическая подложка</h3>
                <p class="text-gray-500 mb-6">
                </p>

                <div class="grid grid-cols-2 gap-3 text-left">
                  <div class="p-3 bg-blue-50 rounded-lg">
                    <div class="font-medium text-blue-700">Точки</div>
                    <div class="text-sm text-blue-600">Отображение координат из БД</div>
                  </div>
                  <div class="p-3 bg-green-50 rounded-lg">
                    <div class="font-medium text-green-700">Линии</div>
                    <div class="text-sm text-green-600">Пути движения объектов</div>
                  </div>
                  <div class="p-3 bg-purple-50 rounded-lg">
                    <div class="font-medium text-purple-700">Маршруты</div>
                    <div class="text-sm text-purple-600">Построение между точками</div>
                  </div>
                  <div class="p-3 bg-orange-50 rounded-lg">
                    <div class="font-medium text-orange-700">Подложка</div>
                    <div class="text-sm text-orange-600">JPG/PNG изображение карты</div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Угловые маркеры (для наглядности) -->
            <div class="absolute top-4 left-4 w-6 h-6 border-2 border-blue-500"></div>
            <div class="absolute top-4 right-4 w-6 h-6 border-2 border-blue-500"></div>
            <div class="absolute bottom-4 left-4 w-6 h-6 border-2 border-blue-500"></div>
            <div class="absolute bottom-4 right-4 w-6 h-6 border-2 border-blue-500"></div>

            <!-- Масштабная линейка (для демонстрации) -->
            <div
              class="absolute bottom-6 left-1/2 transform -translate-x-1/2 bg-black/70 text-white px-3 py-1 rounded-lg text-sm">
              Масштаб: {{ mapScale.toFixed(2) }}x
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Анимации */
@keyframes pulse {

  0%,
  100% {
    opacity: 1;
  }

  50% {
    opacity: 0.5;
  }
}

.animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

/* Плавные переходы для кнопок */
button {
  transition: all 0.2s ease;
}

/* Стили для контейнера карты */
.min-h-\[500px\] {
  min-height: 500px;
}
</style>
