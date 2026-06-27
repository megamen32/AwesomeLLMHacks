# AwesomeLLMHacks
Curaged list of tools and hacks for varius llms: chatgpt, z.ai, deepseek, qwen. 
Dynamic Network Interceptor (Full Stream Support) - Tampermonkey расширение для перехвата всех запросов от ИИ 
- Google AI Studio
- Mistral Chat
- Meta AI
- DeepSeek Chat
- Grok (xAI)
- MiniMax Chat
Разработка/отладка — позволяет видеть, какие запросы отправляются на сервер и что возвращается, в том числе потоковые ответы от нейросетей.
Анализ протоколов — понять, как работают API чат-платформ, какие данные передаются при общении с ИИ.
Ревёрс-инжиниринг — изучение форматов запросов/ответов для интеграции или автоматизации.
Отслеживание WebSocket-соединений — если чат использует веб-сокеты для обмена сообщениями.
Проверка безопасности — наблюдение за тем, какие данные отправляются наружу. Коротко: скрипт делает всю фоновую сетевую активность выбранных ИИ-сайтов видимой для пользователя и даёт возможность гибко реагировать на эти данные прямо из консоли браузера.
Предоставляет объект window.interceptorControl:
По умолчанию все хуки отключены (disable()), скрипт работает «молча».
Вызов enableDefaultLogging() включает подробный вывод в консоль для всех типов событий — можно видеть статусы, тела ответов, куски стрима, WebSocket-сообщения и т.д.
Можно назначить свои функции на каждый хук, например: jsCopyDownload window.interceptorControl.onFetchStreamChunk = (chunkText, url, isDone) => { if (chunkText) console.log('Новый кусок:', chunkText); };
Скрипт даёт прямые JS-хуки (onFetchResponse, onXhrStreamChunk и т.д.), в которых можно выполнять любой код: собирать статистику, сохранять ответы в переменные, выводить алерты при конкретных данных, динамически менять поведение страницы. Фактически это API для сетевых событий внутри страницы.

GPT-AI-Markdown-LaTeX-Copier
A Tampermonkey userscript for copying AI responses as clean Markdown, with better LaTeX formula support.

omniroute - все ваши подписки и api ключи к llm в одном месте

