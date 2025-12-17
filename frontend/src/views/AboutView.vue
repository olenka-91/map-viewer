<template>
  <div class="card">
    <h2 class="text-2xl font-bold text-gray-800 mb-4">О проекте</h2>
    <div class="space-y-4 text-gray-600">
      <p>
        <strong>Map Viewer</strong> — это картографическое приложение для визуализации геоданных,
        разработанное с использованием современных технологий.
      </p>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mt-6">
        <div class="p-4 bg-blue-50 rounded-lg">
          <h3 class="font-bold text-blue-700 mb-2">Frontend</h3>
          <ul class="list-disc pl-5 space-y-1 text-sm">
            <li>Vue 3 с Composition API</li>
            <li>TypeScript для типизации</li>
            <li>Tailwind CSS 4 для стилей</li>
            <li>Pinia для управления состоянием</li>
          </ul>
        </div>

        <div class="p-4 bg-green-50 rounded-lg">
          <h3 class="font-bold text-green-700 mb-2">Backend</h3>
          <ul class="list-disc pl-5 space-y-1 text-sm">
            <li>Go (Golang) для API</li>
            <li>PostgreSQL + PostGIS</li>
            <li>REST API для данных</li>
            <li>WebSocket для обновлений</li>
          </ul>
        </div>
      </div>

      <router-link to="/" class="inline-block mt-6 btn-primary">
        ← Вернуться к карте
      </router-link>
    </div>
  </div>
</template>
