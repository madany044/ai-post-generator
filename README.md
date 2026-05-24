# PostCraft AI — Social Media Post Generator

> AI-powered content generation for 6 platforms, built with LLMs and deployed serverless.

**Live Demo → [ai-post-generators.netlify.app](https://ai-post-generators.netlify.app)**

---

## Overview

PostCraft AI uses a large language model (Google Gemini 2.5) to generate platform-optimized social media content from a single business description. Instead of manually writing different copies for each platform, users describe their product or topic once — the LLM handles tone adaptation, character limits, hashtag strategy, and language style per platform automatically.

Built as a zero-dependency, single-file frontend with a serverless API proxy — no backend server, no framework, no database.

---

## How the AI Works

The core of this project is **prompt engineering** — structuring the LLM prompt to carry brand context, tone, goal, platform rules, and language preference simultaneously. Each generation call passes:

- Business name, industry, target audience, and brand voice as system context
- Platform-specific constraints (e.g. Twitter/X ≤ 280 chars, Instagram hashtag density)
- Tone and goal modifiers to shape the LLM's output style
- Optional A/B instruction to generate two distinct creative angles per platform

The Gemini API call is proxied through a Netlify serverless function — keeping the API key server-side and invisible to the client.

---

## Features

| Feature | Description |
|---|---|
| **Multi-platform generation** | Instagram, LinkedIn, Twitter/X, Facebook, WhatsApp Status, YouTube Community |
| **A/B variants** | Two creative directions per platform for split testing |
| **AI image prompts** | Midjourney / DALL-E style visual prompts generated alongside each post |
| **Brand memory** | Business name, industry, audience and voice saved locally — injected into every prompt |
| **Prompt controls** | 9 tones × 9 goals × 7 languages including Hinglish |
| **Inline editing** | Edit any AI-generated post directly before copying |
| **Post scheduler** | Attach a date and time to each post per platform |
| **Generation history** | Last 30 sessions stored locally and fully restorable |
| **Export** | Download all posts as CSV or JSON |
| **Serverless proxy** | API key never exposed to the client or version control |

---

## Tech Stack

| Layer | Technology |
|---|---|
| **LLM** | Google Gemini 2.5 Flash via REST API |
| **Frontend** | Vanilla HTML5, CSS3, JavaScript — zero dependencies |
| **Serverless function** | Netlify Functions (Node.js) — API proxy |
| **Storage** | Browser localStorage — no database |
| **Deployment** | Netlify (CI/CD via GitHub) |
| **Security** | API key stored as Netlify environment variable |

---

## Why No Framework

Keeping the entire UI in a single HTML file was a deliberate choice — it demonstrates that clean, responsive, and interactive UIs don't require a build pipeline. It also makes the project portable: download one file, open in browser, it works.

---

## Indian Language Support

The LLM prompt is language-aware — switching to Hindi, Hinglish, Kannada, Tamil, Telugu, or Marathi adjusts the generation language while preserving platform formatting rules and brand context. Hinglish in particular performs well for Instagram and WhatsApp audiences in India.

---

## Live Demo

Try it without any setup at **[ai-post-generators.netlify.app](https://ai-post-generators.netlify.app)**
The demo runs on a server-side key — no account or API key needed.

---

<p align="center">Developed and designed by <strong>Madan Y</strong></p>