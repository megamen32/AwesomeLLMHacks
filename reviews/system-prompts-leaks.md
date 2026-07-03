# asgeirtj/system_prompts_leaks

> [github.com/asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks/tree/main) — большая курируемая коллекция реальных system prompts популярных LLM.

## Что это

Репо, в котором собраны **извлечённые и утёкшие** системные промты от основных провайдеров. Не догадки и не реконструкции — фактический текст, который модели получают на старте сессии. Обновляется регулярно: как только появляется новая утёкшая версия, она ложится в репо.

## Покрытие

- **Anthropic** — Claude Opus 4.6–4.8, Sonnet 4.6, Sonnet 5, Claude Fable 5, Claude Code, Claude Design, Claude Cowork, claude.ai Reminders, integration-промты (In Chrome, For Excel, For Word, In PowerPoint, Mobile iOS).
- **OpenAI** — ChatGPT (GPT-5.5 Thinking / Instant / Pro API, GPT-5.4, GPT-5.3, GPT-5.2, GPT-5, GPT-4.5, GPT-4.1, GPT-4o), Codex (CLI, GPT-5.5, 5.4, 5.3, 5.2, 5.1, 5, Plan mode, Personas, Auto-review), tool-промты (Web search, Deep research, Python, Canvas, Image gen, Memory, File search), политики.
- **Google** — Gemini 3.5 Flash, Gemini 3.1 Pro, Gemini CLI, Antigravity CLI, Jules, Gemini YouTube / Workspace / Chrome / Diffusion / Guided learning, AI Studio Build, NotebookLM, Nano / Banana 2.
- **xAI** — Grok Build (CLI agent), Grok 4.3 Beta, 4.2, 4.1, 4, 3, Personas, Account.
- **Perplexity** — Perplexity Computer, Comet Browser, Voice Assistant.
- **Microsoft** — GitHub Copilot, VS Code Copilot Agent, Copilot CLI, Copilot for macOS, Copilot in Word.
- **Cursor**, **Meta AI**, **Mistral Le Chat**, **Notion AI**, **Qwen 3.6 Plus**.
- **Misc** — Amp Code, Docker Gordon AI, ElevenLabs Voice Agent, OpenCode, Reddit Answers, Warp 2.0 Agent, Zed AI, Brave Search, Character AI, Fellou Browser, Kagi Assistant, MiniMax M2.5, Proton Lumo AI, Raycast AI, Sesame AI Maya, t3.chat, t3 Code.

## Зачем

- Увидеть, **как модель на самом деле сконфигурирована** изнутри: роли, tool-use, ограничения, форматы вывода, поведение в edge-cases.
- Использовать реальные промты как базу для собственных override-инструкций (в т.ч. в собственных инструментах из этого awesome-list).
- Понимать, какие инструкции провайдер закладывает в Copilot / Codex / Claude Code — и делать точечные override-хаки.
- Находить тонкие места: форматирование, refusals, tool routing, hidden assumptions.
- Следить за дрейфом: в репо есть diff-страницы между версиями (например, Opus 4.8 → Claude Fable 5).

## Как пользоваться

- Самый быстрый вход — открыть нужную папку провайдера и **сравнить несколько версий подряд**. Сразу видно, что менялось между релизами.
- Для рабочих сценариев — качать конкретный `*.md` и использовать как референс при написании собственных system / developer prompts.
- В Claude Code / Codex можно подгружать эти промты как context, чтобы модель «видела», как она сама настроена изнутри — полезно для prompt-injection / override-экспериментов.
- В репо есть отдельные подпапки `Official/` (опубликованные Anthropic/OpenAI prompt-карты), `raw/` (без обработки), `old/` (архив).

## Ограничения

- Это **утёкшие** промты. Часть из них может быть устаревшей к моменту чтения: модели обновляются чаще, чем репо. Всегда сверяйте дату файла.
- Не все промты реально применяются моделью один-в-один: часть провайдеры скрывают / переписывают рантайм-логикой. Документ — верхушка айсберга.
- Юридически использование чужих system prompts в своих продуктах — серая зона. Для research / обучения — ок, для продакшн-копирования 1:1 — рискованно.
- Репо активно парсят и редактируют — PR-ы приветствуются, но качество контрибьюшенов варьируется.