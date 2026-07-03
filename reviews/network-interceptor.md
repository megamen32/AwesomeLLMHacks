# Dynamic Network Interceptor

> [gist.github.com/Kreijstal/.../fun-user-js](https://gist.github.com/Kreijstal/3b68d94c54e98a22b733e0fe0c739afd) — Tampermonkey-скрипт для перехвата fetch / XHR / WebSocket / SSE / WebRTC на популярных AI-сайтах.

## Что это

UserScript, который прозрачно подвешивает хуки на основные сетевые примитивы браузера и отдаёт управление через объект `window.interceptorControl`. По умолчанию хуки выключены — нужно явно подписаться или вызвать `enableDefaultLogging()`.

## Покрытие

- Google AI Studio (`aistudio.google.com`)
- Mistral Chat (`chat.mistral.ai`)
- Meta AI (`meta.ai`)
- DeepSeek (`chat.deepseek.com`)
- Grok (`grok.com`)
- MiniMax Chat (`chat.minimax.io`)

## Зачем

- Видеть, что именно шлёт и получает веб-интерфейс LLM, без mitm-proxy и DevTools-tracing.
- Отлаживать streaming-ответы (по чанку, не только финал).
- Реверс-инжинирить формат запросов для собственных клиентов / автоматизации.
- Смотреть, какие данные уходят наружу (полезно для аудита приватности).
- Строить свои overlay / логгеры / парсеры поверх реальных сетевых событий.

## API (window.interceptorControl)

Хуки:

- `onXhrResponse(xhr)` — XHR полностью загружен.
- `onXhrStreamChunk(chunk, xhr)` — каждый чанк streaming XHR.
- `onFetchResponse(url, response, responseData)` — Fetch headers получены.
- `onFetchStreamChunk(chunkText, url, isDone)` — каждый чанк streaming Fetch.
- `onWebSocketEvent(event, url)` — входящие WS (`message`, `close` и т.п.).
- `onWebSocketSend(data, url)` — исходящие WS.
- `onWebRTCEvent(pc, eventType, event)` — WebRTC-события.
- `onEventSourceEvent(event, url)` — Server-Sent Events.
- `onBeaconSend(url, data)` — `navigator.sendBeacon`.
- `onResourceLoad(resource)` — общие ресурсы (images, scripts).

Плюс:

- `enableDefaultLogging()` — подробный вывод всех событий в console.
- `disable()` / точечно `onXxx = null` — отключение.

## Пример

```js
window.interceptorControl.onFetchStreamChunk = (chunkText, url, isDone) => {
  if (chunkText) console.log('Stream chunk:', chunkText);
};
```

## Установка

1. Поставить Tampermonkey / Violentmonkey.
2. Создать новый скрипт, вставить код из `fun.user.js` gist-а.
3. Сохранить, открыть поддерживаемый сайт.
4. В DevTools console: `window.interceptorControl.enableDefaultLogging()` — или подписаться на нужные хуки.

## Ограничения

- Это **отладочный** инструмент: перехват трафика в продакшен-страницах может ломать поведение (двойные события, race с самим приложением). Лучше держать включаемым только когда реально нужен.
- Селекторы событий «свои» — в коде нужно держать защиту от двойной загрузки (`window.interceptorLoaded`), иначе дубликат повесит вторую обвязку.
- Не сохраняет историю — только live-stream в console / ваши обработчики. Для долгосрочного логирования писать свой storage.