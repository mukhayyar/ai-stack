# Mukhayyar's AI Stack

Personal AI infrastructure running 24/7 — automations, research, market intelligence, and project tooling.

---

## Infrastructure

| Layer | Detail |
|-------|--------|
| **Host** | Ubuntu VPS (aarch64) |
| **Runtime** | Docker container (`ductor-sandbox`, Debian 12) |
| **Primary Storage** | IDCloudHost S3 (object storage) |
| **Redundant Storage** | Cloudflare R2 (APAC) |
| **Transport** | Telegram Bot API |
| **Network** | Tailscale VPN mesh |
| **DNS / CDN** | Cloudflare |
| **Repo Hosting** | GitHub (`github.com/mukhayyar`) |

---

## Main Agent — Ductor

| Property | Value |
|----------|-------|
| **Framework** | [Ductor Bot](https://github.com/ductorai/ductor) |
| **Model** | Claude Sonnet 4.6 |
| **Memory** | File-based (`MAINMEMORY.md` + refs) + [Mem0](https://github.com/mem-ai/mem0) semantic vector memory |
| **Token Optimization** | [RTK (Rust Token Killer)](https://github.com/rtk-ai/rtk) — 60–90% savings |
| **Voice Transcription** | [faster-whisper](https://github.com/SYSTRAN/faster-whisper) (local, no API key) |

### Capabilities

- 💬 Conversational assistant via Telegram
- 🗂️ Persistent file workspace
- 🧠 Semantic long-term memory (Mem0 + local vector search)
- 🔧 Background task delegation (autonomous sub-processes)
- 📅 Cron job scheduling & webhook handling
- 🤖 Multi-agent orchestration
- 🎙️ Local voice transcription (faster-whisper)
- 🖥️ Remote Windows PC control via Tailscale
- 🐙 GitHub repo management (gh CLI — create repos, PRs, issues)
- ☁️ Cloudflare management (DNS, R2 storage, zones via API)

---

## Sub-Agents

### ResearchBot

| Property | Value |
|----------|-------|
| **Model** | Claude Sonnet 4.6 |
| **Role** | Academic paper research, citations, literature review, draft writing |
| **Sources** | PubMed · arXiv · Europe PMC · bioRxiv · Semantic Scholar · Unpaywall |
| **Output** | Papers auto-uploaded to object storage |
| **Specialty** | Edge AI, computer vision, ML inference optimization |

---

## Automated Jobs (Cron)

| Job | Schedule | Model | Description |
|-----|----------|-------|-------------|
| 📈 IHSG Daily Summary | Weekdays, market close | Haiku | IDX market close — energy sector, small caps, top movers |
| ☀️ Morning News Digest | Daily, 06:00 JST | Haiku | Top stories across Tech, Business, Politics, Developer |
| 🚨 Breaking News Monitor | Every 15 min, 24/7 | Haiku | High-impact alerts only — Indonesia / Japan / Global |
| 📊 Commodities Report | Every 3 hours, 24/7 | Haiku | 23 assets — energy, metals, agriculture, FX, crypto |
| 📉 PasarWatch RL Update | Daily, market close | Haiku | Per-ticker RL model training for IDX watchlist |

---

## PasarWatch — Stock Intelligence

Prophet forecasting + per-ticker RL model for IDX penny stocks.

| Property | Detail |
|----------|--------|
| **Forecasting** | Prophet (logistic growth, floor=0, cap=3×max — prevents negative prices) |
| **RL Model** | Per-ticker Q-learning, 7 features, trained daily |
| **Sentiment** | HuggingFace financial sentiment (real headlines per ticker) |
| **Chart** | MA5/20, RSI(14), volume ratio, 5d return, Prophet 7d/30d bands |

---

## Skills

| Skill | Status | Description |
|-------|--------|-------------|
| `news-aggregator` | ✅ Active | 23 RSS feeds, regional tagging, breaking news detection |
| `commodities-tracker` | ✅ Active | yfinance + RSS, WTI/Brent/Gold/CPO/BTC/ETH |
| `personal-assistant` | ✅ Active | Daily briefings, tasks, Google Workspace (Gmail/Calendar/Tasks) |
| `cfo` | ✅ Active | Financial planning — IDR/JPY, IHSG, crypto, budgeting |
| `inventory` | ✅ Active | Physical asset tracking |
| `moltbook` | ⏸️ Paused | Social agent on Moltbook as `@ductorai` |

---

## Remote PC Control

| Property | Detail |
|----------|--------|
| **Access** | Tailscale VPN → SSH → local HTTP agent |
| **Endpoints** | screenshot, click, type, hotkey, run, navigate, windows |
| **Libraries** | pyautogui, win32gui, pygetwindow, opencv |
| **Auto-start** | VBScript in Windows Startup folder |
| **⚠️ Note** | Must start via VBScript (interactive session) — SSH restart breaks keyboard/mouse |

---

## Object Storage

| | IDCloudHost S3 | Cloudflare R2 |
|--|--|--|
| **Role** | Primary | Redundancy |
| **Region** | Jakarta | APAC |
| **Protocol** | S3-compatible | S3-compatible |

---

## Local ML Models (CPU)

| Model | Task |
|-------|------|
| `cardiffnlp/twitter-roberta-base-sentiment-latest` | Sentiment analysis |
| `mrm8488/distilroberta-finetuned-financial-news-sentiment` | Financial sentiment |
| `cross-encoder/nli-MiniLM2-L6-H768` | Zero-shot classification |
| `sshleifer/distilbart-cnn-12-6` | Summarization |
| `dslim/bert-base-NER` | Named entity recognition |
| `Helsinki-NLP/opus-mt-id-en` | Indonesian → English translation |
| `deepset/roberta-base-squad2` | Document Q&A |
| `multi-qa-MiniLM-L6-cos-v1` | Semantic embeddings (Mem0) |

---

## Tech Stack

```
LLMs          Claude Sonnet 4.6, Claude Haiku 4.5
Framework     Ductor Bot
Transport     Telegram Bot API (aiogram)
Languages     Python
Storage       IDCloudHost S3 (primary) + Cloudflare R2 (redundancy)
Memory        Mem0 — Qdrant vector DB + sentence-transformers
ML Models     HuggingFace Transformers (CPU, local)
Forecasting   Prophet (logistic growth)
Voice         faster-whisper (local, base model)
Data          yfinance, feedparser, beautifulsoup4
Infra         Docker on Ubuntu VPS (aarch64, CPU-only)
Network       Tailscale VPN
DNS/CDN       Cloudflare
Source        GitHub — gh CLI (full API: repos, PRs, issues)
PC Control    pyautogui, win32gui (via Tailscale)
Token Opt.    RTK — Rust Token Killer
```

---

*Last updated: March 2026*
