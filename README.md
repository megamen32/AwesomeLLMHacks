# AwesomeLLMHacks

> Куратированный список инструментов и хаков для работы с LLM-сервисами в браузере: ChatGPT, Z.AI, DeepSeek, Qwen, Claude, Grok, Google AI Studio и др.

Фокус — прикладные штуки, которые помогают в ежедневной работе с веб-интерфейсами моделей: многопанельный ChatGPT, очереди промптов, перехват сетевого трафика, копирование в чистый Markdown, агрегация провайдеров, референс по реальным system prompts.

Полный разбор каждого инструмента — в [`reviews/`](reviews/). Короткие карточки ниже.

## Contents

- [Chrome Extensions](#chrome-extensions)
- [Tampermonkey / UserScripts](#tampermonkey--userscripts)
- [Provider Routing & Gateways](#provider-routing--gateways)
- [Reference: System Prompts](#reference-system-prompts)

## Chrome Extensions

- [chatgpt-multi](https://github.com/megamen32/chatgpt-multi) — несколько параллельных панелей ChatGPT в одном workspace, с lazy-pane и conversation trim. → [📄 review](reviews/chatgpt-multi.md)
- [auto-confirm-extension](https://github.com/megamen32/auto-confirm-extension) — автоклик по диалогам подтверждения в Custom GPT actions. → [📄 review](reviews/auto-confirm-extension.md)
- [promqueue](https://github.com/megamen32/promqueue) — очередь и bulk-send промптов в z.ai, ChatGPT, Claude, DeepSeek, Qwen, Gemini, AI Studio, Copilot. → [📄 review](reviews/promqueue.md)
- [zai-auto-retry](https://github.com/megamen32/zai-auto-retry) — автоповтор запроса в Z.AI при появлении peak-hours диалога. → [📄 review](reviews/zai-auto-retry.md)

## Tampermonkey / UserScripts

- [Dynamic Network Interceptor](https://gist.github.com/Kreijstal/3b68d94c54e98a22b733e0fe0c739afd) — перехват fetch/XHR/WebSocket/SSE на AI Studio, Mistral, Meta, DeepSeek, Grok, MiniMax. → [📄 review](reviews/network-interceptor.md)
- [GPT-AI-Markdown-LaTeX-Copier](https://github.com/Wavesflow/GPT-AI-Markdown-LaTeX-Copier) — копирование ответов LLM в чистый Markdown с сохранением LaTeX. → [📄 review](reviews/markdown-latex-copier.md)

## Provider Routing & Gateways

- [OmniRoute](https://github.com/diegosouzapw/OmniRoute) — единый endpoint для 237 LLM-провайдеров (90+ бесплатных), RTK-компрессия, auto-fallback, MCP/A2A. → [📄 review](reviews/omniroute.md)

## Reference: System Prompts

- [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks/tree/main) — большая коллекция реальных system prompts от Anthropic, OpenAI, Google, xAI, Cursor, Copilot, Perplexity, Qwen, Mistral, Meta, Microsoft, Notion. → [📄 review](reviews/system-prompts-leaks.md)

## Contributing

PR-ы приветствуются. Формат: одна строка `— [name](url) — tagline → [📄 review](reviews/<slug>.md)`, плюс обзор в `reviews/<slug>.md` с разделами «Что это», «Зачем», «Установка», «Как использовать», «Ограничения».

## License

MIT.