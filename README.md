# ChatBox

A lightweight, single-file chat client for OpenAI-compatible APIs. No build tools, no dependencies to install — just one HTML file.

![HTML5](https://img.shields.io/badge/HTML5-single--file-E34F26?logo=html5&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue)

## Features

- **Single HTML File** — Zero build step. Open in any browser and start chatting.
- **OpenAI-Compatible** — Works with any API that follows the OpenAI chat completions format (OpenAI, DeepSeek, Claude via proxy, local models, etc.).
- **Streaming Responses** — Real-time token-by-token rendering via Server-Sent Events (SSE).
- **Thinking / Reasoning** — Displays `reasoning_content` in a collapsible block with a spinning indicator during generation.
- **Markdown & Code Highlighting** — Full GFM support powered by [marked](https://github.com/markedjs/marked) + [highlight.js](https://github.com/highlightjs/highlight.js), with one-click copy on code blocks.
- **Multi-Model Selector** — Configure multiple models and switch between them from the header dropdown.
- **Chat History** — Conversations persist in `localStorage`, grouped by date (Today / Yesterday / Last 7 days / Earlier).
- **SSE Stream Parser** — Import raw SSE stream data by pasting or selecting a file — automatically assembles and renders the final output as a new conversation.
- **Export** — One-click export of all chat logs as JSON.
- **Dark Theme** — Clean dark UI inspired by modern chat applications.
- **Mobile Responsive** — Collapsible sidebar adapts to small screens.

## Quick Start

1. Download `chat.html` (or clone this repo).
2. Open it in a browser.
3. Click **⚙ Settings** and configure:

| Field | Description |
|-------|-------------|
| **Endpoint** | Your API endpoint, e.g. `https://api.openai.com/v1/chat/completions` |
| **API Key** | Your API key (`sk-...`) |
| **Models** | One model per line. Format: `value:label` or just `value` |

4. Start chatting.

## SSE Stream Parser

Parse raw SSE streaming responses into rendered messages — useful for debugging, log analysis, or reviewing saved API responses.

**Usage:**

1. Click **解析流式文件** in the sidebar.
2. Paste SSE data directly into the textarea, or click **选择文件** to load a `.txt` / `.log` / `.json` file.
3. Click **解析** — the assembled result renders as a new conversation with full Markdown, thinking blocks, and token stats.

**Supported format:**

```
data: {"choices":[{"delta":{"content":"Hello"}}],"model":"gpt-4o","id":"chatcmpl-xxx"}

data: {"choices":[{"delta":{"content":" world"}}],"model":"gpt-4o","id":"chatcmpl-xxx"}

data: [DONE]
```

Also supports `reasoning_content` (DeepSeek, QwQ, etc.) and `usage` fields.

## Security

| Measure | Detail |
|---------|--------|
| **XSS Protection** | All Markdown output sanitized via [DOMPurify](https://github.com/cure53/DOMPurify). Dynamic values in stats are HTML-escaped. |
| **HTTPS Check** | Warns before saving a non-HTTPS endpoint (excludes `localhost` / `127.0.0.1`). |
| **Local Storage Only** | No data leaves the browser. API key and chat history stay in `localStorage`. |
| **No Tracking** | Zero analytics, telemetry, or external requests beyond the configured API endpoint and CDN libraries. |

## Tech Stack

| Component | Library |
|-----------|---------|
| Markdown | [marked 9.1.6](https://github.com/markedjs/marked) (CDN) |
| Syntax Highlighting | [highlight.js 11.9.0](https://github.com/highlightjs/highlight.js) (CDN) |
| XSS Sanitization | [DOMPurify 3.0.6](https://github.com/cure53/DOMPurify) (CDN) |
| Everything else | Vanilla JS, CSS, HTML |

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Enter` | Send message |
| `Shift + Enter` | New line |

## Data Storage

All data is stored in the browser's `localStorage`:

| Key | Content |
|-----|---------|
| `chat_logs` | Array of all conversations (messages, timestamps, stats) |
| `chatbox_config` | Endpoint, API key, model list |
| `chatbox_last_model` | Last selected model |

Session state (`current_chat_id`) uses `sessionStorage` and resets on tab close.

## License

MIT
