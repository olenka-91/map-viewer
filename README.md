Map Viewer / Geo Tracker

Картографическое приложение для отображения и построения маршрутов.

## Структура проекта
- `frontend/` - Vue 3 приложение на TypeScript
- `backend/` - Go сервер с API
- `docs/` - документация

## Технологии
- **Frontend:** Vue 3, TypeScript, Pinia, возможно Leaflet/OpenLayers
- **Backend:** Go (Gin/Fiber), PostgreSQL, PostGIS
- **База данных:** PostgreSQL с расширением PostGIS

## Быстрый старт
1. Клонировать репозиторий
2. Настроить окружение (см. docs/setup.md)
3. Запустить backend: `cd backend && go run main.go`
4. Запустить frontend: `cd frontend && pnpm dev`

## TODO
- [ ] Настройка проекта
- [ ] Базовый API
- [ ] Отображение подложки
- [ ] Работа с точками и линиями
- [ ] Построение маршрутов