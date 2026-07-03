# chatgpt-multi

> [github.com/megamen32/chatgpt-multi](https://github.com/megamen32/chatgpt-multi) — многопанельный ChatGPT workspace с lazy-pane, conversation trim, queue, goal-agent и Telegram-мостом.

## Что это

Chrome-расширение, в котором ChatGPT открывается не одной линейной перепиской, а несколькими параллельными iframe-панелями в одном workspace. Каждая панель — живой `chatgpt.com`, поэтому продолжают работать model picker, deep research, composer и streaming.

## Зачем

- Сравнивать ответы разных моделей или разных промптов рядом, а не в куче вкладок.
- Держать раздельно «план / код / проверка / финал», чтобы контексты не перемешивались.
- Гонять подготовленные промпты через очередь, не теряя общий контекст.
- Превращать ChatGPT в нормальный многозадачный рабочий стол.

## Архитектура (важно)

- **Lazy panes** — iframe монтируется только у сфокусированной панели, остальные показывают placeholder. Кнопка ☾ на панели выгружает iframe и освобождает память.
- **Conversation trim** — MAIN-world content script патчит `fetch`, обрезая `GET /backend-api/conversation/{id}` до последних N сообщений активной ветки. Длинные чаты перестают фризиться.
- **Settings bridge** — ISOLATED-world скрипт зеркалит настройки в `<html>` dataset, MAIN-world patch их читает. Оба инжектятся с `all_frames: true`, поэтому работают внутри iframe-панелей (это ломало standalone-расширения).

## Фичи (всё тогглится в настройках)

- Native chat picker: `+` панель показывает список чатов через `/backend-api/conversations` без полной загрузки.
- Title / URL sync: имя панели = имя чата, переживает SPA-навигацию и reload.
- Auto-confirm Custom GPT actions + auto-expand tool calls.
- Prompt queue с auto-send, когда ChatGPT idle.
- Auto-collapse старых сообщений в активной панели.

## Goal Agent + Telegram

- **🎯 Goal Agent** — focused pane = executor, вторая pane = evaluator. После каждого хода executor-а controller извлекает только финальный ответ (без tool calls/reasoning) и спрашивает agent-а в свежем чате с **memory disabled**, достигнута ли цель. Marker `GOAL REACHED GOAL` останавливает цикл. Memory отключается PATCH-ем account settings перед каждым ходом agent-а.
- **Telegram bridge** — bot token + user id в настройках. Service worker long-poll-ит Telegram на 1-min alarm (переживает рестарты), шлёт сообщения чанками по 4096. 📤 зеркалит ответы панели в Telegram, входящие Telegram-сообщения идут в executor.

## Установка

1. `chrome://extensions` → включить Developer mode.
2. Load unpacked → выбрать папку репо.
3. Открыть иконку расширения или `chrome-extension://<id>/app.html`.

Если ChatGPT меняет CSP/frame behaviour — обновлять `src/rules/*.json`.

## Тесты

```
npm test          # unit + perf (node:test, без зависимостей)
npm run test:perf # только perf
```

Покрывают алгоритм trim (включая budget 4000→20 сообщений) и state machine панелей.

## Ограничения

- Расширение опирается на внутренние endpoints ChatGPT (`/backend-api/conversations`, `/backend-api/conversation/{id}`). При их изменении часть фич ломается до апдейта rules.
- Все панели шарят одну сессию ChatGPT (один аккаунт, одна модель по умолчанию).
- Memory-disable для Goal Agent работает через PATCH аккаунт-settings — это side-effect на профиль, не локальное переключение.