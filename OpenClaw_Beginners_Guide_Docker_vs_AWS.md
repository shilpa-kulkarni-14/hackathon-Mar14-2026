# OpenClaw Setup Guide: Docker vs AWS -- What You Need to Know

### A plain-language guide for women getting started with AI tools -- with security front and center.

---

## Table of Contents

1. [Before We Start: What Even Is OpenClaw?](#1-before-we-start-what-even-is-openclaw)
2. [What Can OpenClaw Actually DO? (Real Use Cases)](#2-what-can-openclaw-actually-do)
3. [OpenClaw vs Claude Code vs Cursor vs Copilot -- What's the Difference?](#3-openclaw-vs-claude-code-vs-cursor-vs-copilot)
4. [Can I Use OpenClaw 100% Free? (Yes, Here's How)](#4-can-i-use-openclaw-100-free)
5. [What You Need Before You Start (API Keys, Accounts & Costs)](#5-what-you-need-before-you-start)
6. [Free vs Paid: What Do You Actually Get?](#6-free-vs-paid-what-do-you-actually-get)
7. [Do I HAVE to Use the Terminal? (GUI & No-Code Options)](#7-do-i-have-to-use-the-terminal)
8. [What Is Docker? (And Why Should I Care?)](#8-what-is-docker-and-why-should-i-care)
9. [What Is AWS? (The Cloud, Demystified)](#9-what-is-aws-the-cloud-demystified)
10. [Docker vs AWS: The Full Comparison](#10-docker-vs-aws-the-full-comparison)
11. [Security Deep Dive: Where Does My Data Go?](#11-security-deep-dive-where-does-my-data-go)
12. [Which One Should I Choose?](#12-which-one-should-i-choose)
13. [Glossary: Tech Terms in Plain English](#13-glossary-tech-terms-in-plain-english)

---

# 1. Before We Start: What Even Is OpenClaw?

OpenClaw is an **open-source AI agent** that runs on your own machine and connects to the **messaging apps you already use** -- WhatsApp, Telegram, Slack, Discord, Signal, iMessage, Microsoft Teams, and more (12+ platforms total).

Think of it this way:

> **ChatGPT/Claude website** = You go to a website and type questions.
> **OpenClaw** = An AI assistant that lives inside your WhatsApp/Telegram/Slack and can actually *do things* for you -- send emails, manage files, check your calendar, fill out forms, monitor websites, and work while you sleep.

The key difference: ChatGPT is a chatbot you visit. **OpenClaw is an agent that lives in your life.**

It's free, open-source (anyone can inspect the code), and runs on your own hardware so your data stays private. It was created by Peter Steinberger and has grown to ~296,000 GitHub stars, making it one of the most popular open-source AI projects in the world.

**Why does it need "setup"?**
Unlike apps you download from the App Store, OpenClaw is a developer tool. It needs a little technical setup to run. There are two ways to run it:


| Option                      | One-Line Summary                                                                                           |
| --------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Docker (on your laptop)** | OpenClaw runs inside a secure box on YOUR computer. Nothing leaves your machine.                           |
| **AWS (in the cloud)**      | OpenClaw runs on a rented computer in Amazon's data center. It stays on 24/7 even when your laptop is off. |


Both work. The right choice depends on your comfort level and what you need.

---

# 2. What Can OpenClaw Actually DO?

This is the most important section. If you're investing time to set this up, you should know what you're getting.

## The One-Sentence Version

OpenClaw is like hiring a digital personal assistant that works 24/7, lives inside your messaging apps, and never sleeps.

## Real Use Cases (What People Actually Do With It)

### Everyday Life

| What You Tell OpenClaw | What It Does |
|---|---|
| "Remind me to call the dentist tomorrow at 9am" | Sets a reminder and messages you at 9am via WhatsApp/Telegram |
| "Add milk, eggs, and bread to my grocery list" | Maintains a shared list, can even auto-detect groceries mentioned in your family chat |
| "What's my schedule today?" | Checks your calendar and sends you a formatted summary |
| "Send Mom a birthday message" | Drafts and sends a personalized message through your messaging app |
| "Check if my flight is on time" | Looks up your flight status and alerts you of changes |

### Work & Productivity

| What You Tell OpenClaw | What It Does |
|---|---|
| "Summarize the 47 emails I got overnight" | Reads your inbox, categorizes by urgency, and gives you a 2-minute summary |
| "Draft a reply to Sarah's email about the Q3 report" | Writes a professional reply for your review before sending |
| "Remind the team about Friday's deadline" | Sends personalized reminders to team members via Slack/Teams |
| "Find all invoices from January in my email" | Searches and compiles them for you |
| "Transcribe this voice recording from the meeting" | Converts speech to text and formats it into meeting notes |

### Smart Automation (The "Wow" Stuff)

| What It Can Do | How It Works |
|---|---|
| **Daily morning briefing** | Every morning at 7am, sends you: weather, calendar, top tasks, news headlines, health stats |
| **Email cleanup on autopilot** | One user cleared 4,000+ emails in 2 days -- OpenClaw unsubscribed from spam, categorized by urgency, drafted replies |
| **Podcast workflow** | Research guests, create outlines, generate show notes, draft social media posts -- all from one prompt |
| **Web monitoring** | Watch a product page and alert you when the price drops below a target |
| **File organization** | Sort your Downloads folder, rename files with consistent naming, move to appropriate folders |

### For the Hackathon Specifically

| Hackathon Task | How OpenClaw Helps |
|---|---|
| "Research what technologies other teams used for similar projects" | Searches the web and summarizes findings |
| "Help me brainstorm ideas for our project" | Interactive brainstorming session via your messaging app |
| "Write a project description for our submission" | Drafts, revises, and polishes your writeup |
| "What time does the hackathon end? What's the submission format?" | Quick reference without searching through emails |
| "Help me debug this error" | Analyzes error messages and suggests fixes |

## What Apps Does OpenClaw Connect To?

```
Your Phone/Computer
        │
        ├── WhatsApp ──────┐
        ├── Telegram ──────┤
        ├── Slack ─────────┤
        ├── Discord ───────┤
        ├── Signal ────────┤      ┌──────────────┐
        ├── iMessage ──────┼─────►│   OpenClaw    │
        ├── Microsoft Teams┤      │   (running    │
        ├── Google Chat ───┤      │   on your     │
        ├── Matrix ────────┤      │   machine)    │
        ├── IRC ───────────┤      └──────┬───────┘
        ├── LINE ──────────┤             │
        └── Web Chat ──────┘             ▼
                                    AI Brain
                                 (Claude/GPT/Gemini)
```

You pick whichever app you already use. OpenClaw meets you where you are.

## What OpenClaw is NOT

Let's be clear so there's no confusion:

- It is **not** a website you visit (like ChatGPT.com)
- It is **not** a code editor (like Cursor or VS Code)
- It is **not** an app builder (like Lovable)
- It is **not** a chatbot with pre-programmed responses
- It **is** an autonomous agent that takes real actions on your behalf

---

# 3. OpenClaw vs Claude Code vs Cursor vs Copilot

If you've heard of tools like Claude Code, Cursor, or GitHub Copilot, you might wonder: "Is OpenClaw the same thing? Do I need all of them?"

Here's the honest breakdown:

## They Solve Completely Different Problems

Think of it like this:

> **OpenClaw** = Your personal assistant (handles your life -- messages, emails, scheduling, automation)
> **Claude Code** = Your coding partner (helps you write software at the terminal)
> **Cursor** = Your smart text editor (helps you edit code files with AI suggestions)
> **GitHub Copilot** = Your autocomplete on steroids (suggests code as you type)

They're like a personal assistant, a tutor, a word processor, and a spell checker. They all use AI, but they do very different things.

## Side-by-Side Comparison


| Feature | OpenClaw | Claude Code | Cursor | GitHub Copilot |
|---|---|---|---|---|
| **What it does** | Personal/work automation agent | Terminal-based coding assistant | AI-powered code editor | Code autocompletion |
| **Where it lives** | Your messaging apps (WhatsApp, Slack, etc.) | Your terminal (command line) | Desktop app (like VS Code) | Plugin inside your editor |
| **Main job** | Automate tasks across your digital life | Help you build and debug software | Help you edit code files | Suggest the next line of code |
| **Manages email?** | Yes | No | No | No |
| **Manages calendar?** | Yes | No | No | No |
| **Writes code?** | Can do basic coding tasks | Expert-level coding | Expert-level coding | Good at suggestions |
| **Works while you sleep?** | Yes (always-on agent) | No (interactive tool) | No (interactive tool) | No (interactive tool) |
| **Requires coding knowledge?** | No | Yes | Yes | Yes |
| **Cost** | Free + API costs ($0-15/mo) | Free (with own API key) or $20/mo | $20/mo | $10/mo |
| **Best for** | Everyone (especially non-coders) | Developers | Developers | Developers |


## Can You Use Them Together?

**Yes, and that's the recommended approach for developers.**

```
Morning:
  └── OpenClaw (via WhatsApp): "What's on my plate today?"
      └── Sends you: calendar, emails summary, pending tasks

Work Session:
  └── Claude Code (in terminal): "Refactor the payment module"
      └── Rewrites code across multiple files

  └── Cursor (in editor): Editing files with AI suggestions

  └── Copilot (in editor): Auto-completing as you type

Evening:
  └── OpenClaw (via Telegram): "Summarize what I worked on today and draft a standup message"
      └── Creates your standup update, ready for tomorrow morning
```

**OpenClaw handles your life. Coding tools handle your code.** They complement each other perfectly.

## Do You Need a Paid Subscription to Any of These to Use OpenClaw?

**No.** OpenClaw is completely independent. You do NOT need:
- A paid Claude Code subscription
- A paid Cursor subscription
- A paid Copilot subscription
- ANY other tool subscription

OpenClaw only needs an API key from an AI provider (which can be **completely free** -- see next section).

---

# 4. Can I Use OpenClaw 100% Free?

**Yes.** Here are three ways to run OpenClaw at absolute zero cost:

## Option A: OpenClaw + Google Gemini Free Tier (Easiest)

| Component | Cost |
|---|---|
| OpenClaw software | $0 (open source) |
| Docker Desktop | $0 (free for personal use) |
| Google Gemini API key | $0 (free tier, no credit card) |
| **Total** | **$0** |

**How:** Sign in to [aistudio.google.com](https://aistudio.google.com) with your Google account, click "Get API Key," paste it into OpenClaw's config. Done.

**What you get:** 1,000 requests/day with Gemini 2.5 Pro (one of the best AI models available). That's more than enough for a hackathon or daily personal use.

**The catch:** Google's free tier may use your data to improve their products. If that's a concern, see Option B or C.

## Option B: OpenClaw + OpenRouter Free Models

| Component | Cost |
|---|---|
| OpenClaw software | $0 |
| Docker Desktop | $0 |
| OpenRouter API key | $0 (free models available, no credit card needed) |
| **Total** | **$0** |

**How:** Create a free account at [openrouter.ai](https://openrouter.ai), generate an API key, configure OpenClaw to use it.

**What you get:** Access to 24+ free models from Google, Meta, Mistral, NVIDIA, and others. You can try different AI "brains" and see which one you like best.

**The catch:** Rate limited to 20 requests/minute and 200 requests/day. Fine for testing, tight for heavy use.

## Option C: OpenClaw + Ollama Local Models (Maximum Privacy)

| Component | Cost |
|---|---|
| OpenClaw software | $0 |
| Docker Desktop | $0 |
| Ollama (local AI) | $0 (runs AI models on your own hardware) |
| API key | Not needed (use any placeholder value) |
| **Total** | **$0** |

**How:** Install Ollama, download a model (e.g., `ollama pull qwen3`), configure OpenClaw to use it.

**What you get:** The AI runs entirely on YOUR computer. Nothing goes to the internet -- not even your prompts. Maximum possible privacy.

**The catch:** Requires a decent computer (8GB+ RAM). Smaller local models aren't as smart as cloud models like Claude or GPT-4. Great for simple tasks, less great for complex reasoning.

## The Minimum You Need to Get Running

Here's the absolute minimum checklist:

```
✅ A computer (Mac, Windows, or Linux)
✅ Docker Desktop installed (free download)
✅ ONE free API key (Google Gemini is easiest)
✅ 20 minutes of setup time

That's it. Total cost: $0.
```

## When Does It Start Costing Money?

| Situation | Cost |
|---|---|
| Hackathon (1 day, moderate use, Gemini free) | $0 |
| Hackathon (1 day, moderate use, Claude Sonnet) | $1-3 |
| Weekly casual use (Gemini free) | $0 |
| Weekly casual use (Claude Sonnet) | $5-10/month |
| Daily power use (Claude Sonnet) | $15-30/month |
| Running 24/7 on AWS + Claude | $20-40/month |

**For this hackathon, you can do everything for free.**

---

# 5. What You Need Before You Start

Before you can use OpenClaw, you need **two things**: the software itself (free) and an **API key** to connect it to an AI brain. Think of it this way:

> **OpenClaw** = the car
> **API key** = the fuel
> Without fuel, the car doesn't move. Without an API key, OpenClaw can't think.

## What Is an API Key?

An API key is a long string of random characters (like `sk-ant-api03-xYz123...`) that acts as your **personal pass** to use an AI service. When you sign up with an AI provider (Anthropic, Google, OpenAI), they give you this key. You paste it into OpenClaw's settings, and now OpenClaw can send your questions to that AI and get answers back.

**It's like a library card.** The library (AI provider) gives you a card (API key). You show the card every time you borrow a book (ask a question). The library tracks how many books you've borrowed (usage) and may charge you if you go over the free limit.

## Your AI Provider Options

You only need **ONE** of these. Pick the one that feels right for your situation:

### Option 1: Google Gemini -- The Best Free Starting Point


| Detail                   | Info                                                                                                            |
| ------------------------ | --------------------------------------------------------------------------------------------------------------- |
| **Cost**                 | Genuinely free. No credit card needed.                                                                          |
| **How to get it**        | Go to [aistudio.google.com](https://aistudio.google.com), sign in with your Google account, click "Get API Key" |
| **Key looks like**       | `AIzaSy...`                                                                                                     |
| **Environment variable** | `GEMINI_API_KEY`                                                                                                |
| **Free tier limits**     | 15 requests/minute, up to 1,000 requests/day, full 1 million token context window                               |
| **Models included free** | Gemini 2.5 Pro, Gemini 2.5 Flash, Gemini 2.0 Flash                                                              |
| **Best for**             | Beginners who want to try with zero financial commitment                                                        |
| **Privacy note**         | Free tier data *may* be used by Google to improve their products. If this concerns you, consider a paid option. |


**Why this is great for beginners:** You already have a Google account. You don't enter a credit card. If you decide AI isn't for you, you've spent $0. The models are genuinely capable -- Gemini 2.5 Pro is one of the top AI models available.

---

### Option 2: OpenRouter -- The Free Buffet


| Detail                   | Info                                                                                            |
| ------------------------ | ----------------------------------------------------------------------------------------------- |
| **Cost**                 | Free tier available. No credit card needed for free models.                                     |
| **How to get it**        | Go to [openrouter.ai](https://openrouter.ai), create account, generate API key                  |
| **Key looks like**       | `sk-or-v1-...`                                                                                  |
| **Environment variable** | `OPENROUTER_API_KEY`                                                                            |
| **Free tier limits**     | 20 requests/minute, 200 requests/day                                                            |
| **Models included free** | 24+ free models from Google, Meta, Mistral, NVIDIA, and others                                  |
| **Best for**             | People who want to try multiple AI models without paying for each one separately                |
| **Privacy note**         | Free models are provided by their respective companies; OpenRouter routes your request to them. |


**What makes this unique:** OpenRouter is like a food court -- one entrance, many restaurants. With one API key, you can try models from Google, Meta, Mistral, and more. Some are free, some cost money. You pick per-request.

---

### Option 3: Anthropic Claude -- The Security-Conscious Choice


| Detail                   | Info                                                                                                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **Cost**                 | $5 free credits for new accounts (no expiration). After that, pay-as-you-go.                                 |
| **How to get it**        | Go to [console.anthropic.com](https://console.anthropic.com), create account, go to API Keys, create new key |
| **Key looks like**       | `sk-ant-api03-...`                                                                                           |
| **Environment variable** | `ANTHROPIC_API_KEY`                                                                                          |
| **Credit card needed?**  | Not for the initial $5 credit. Required after that.                                                          |
| **Models available**     | Claude Haiku (fast/cheap), Claude Sonnet (balanced), Claude Opus (most capable)                              |
| **Best for**             | Strong coding help, nuanced reasoning, safety-focused AI                                                     |
| **Privacy note**         | Anthropic does NOT use your API data to train models. Your conversations are private.                        |


**Typical costs after free credits:**


| Model             | What it costs per ~750 words you send | What it costs per ~750 words it replies |
| ----------------- | ------------------------------------- | --------------------------------------- |
| Claude Haiku 4.5  | ~$0.001 (one-tenth of a penny)        | ~$0.005                                 |
| Claude Sonnet 4.5 | ~$0.003                               | ~$0.015                                 |
| Claude Opus 4.5   | ~$0.005                               | ~$0.025                                 |


For a typical hackathon day of moderate use, expect to spend **$1-3 total** with Claude Sonnet.

---

### Option 4: OpenAI (ChatGPT) -- The Familiar Name


| Detail                   | Info                                                                                     |
| ------------------------ | ---------------------------------------------------------------------------------------- |
| **Cost**                 | $5 free credits for new accounts (expire after 3 months). Then pay-as-you-go.            |
| **How to get it**        | Go to [platform.openai.com](https://platform.openai.com), create account, go to API Keys |
| **Key looks like**       | `sk-proj-...`                                                                            |
| **Environment variable** | `OPENAI_API_KEY`                                                                         |
| **Credit card needed?**  | Not for initial credits. Required after.                                                 |
| **Models available**     | GPT-4o (flagship), GPT-4o-mini (budget)                                                  |
| **Best for**             | General purpose, wide ecosystem, familiar brand                                          |
| **Privacy note**         | API data is NOT used for training by default (different from the ChatGPT website).       |


**Typical costs:**


| Model       | Cost per ~750 words you send | Cost per ~750 words it replies |
| ----------- | ---------------------------- | ------------------------------ |
| GPT-4o-mini | ~$0.0002 (tiny)              | ~$0.0006                       |
| GPT-4o      | ~$0.0025                     | ~$0.01                         |


GPT-4o-mini is extremely cheap. For a full hackathon day, you might spend **under $1**.

---

### Option 5: DeepSeek -- The Budget Power Option


| Detail                   | Info                                                                                         |
| ------------------------ | -------------------------------------------------------------------------------------------- |
| **Cost**                 | Pay-as-you-go. Extremely cheap.                                                              |
| **How to get it**        | Go to [platform.deepseek.com](https://platform.deepseek.com), create account, generate key   |
| **Key looks like**       | `sk-...`                                                                                     |
| **Environment variable** | `DEEPSEEK_API_KEY`                                                                           |
| **Cost**                 | ~$0.28 per million input tokens (roughly 10x cheaper than GPT-4o)                            |
| **Best for**             | Budget-conscious users who want strong performance                                           |
| **Privacy note**         | DeepSeek is a Chinese company. If data jurisdiction matters to you, consider another option. |


---

## Quick Decision: Which API Key Should I Get?

```
Start here:
    │
    ├── "I don't want to spend anything or enter a credit card"
    │       └── ✅ Google Gemini (free tier) or OpenRouter (free models)
    │
    ├── "I care most about privacy -- my data should NOT train AI models"
    │       └── ✅ Anthropic Claude ($5 free, no training on your data)
    │
    ├── "I want the cheapest option that still works well"
    │       └── ✅ OpenAI GPT-4o-mini or DeepSeek
    │
    ├── "I want to try different models and compare"
    │       └── ✅ OpenRouter (one key, 400+ models)
    │
    └── "I just want the easiest, most familiar option"
            └── ✅ OpenAI (you may already have an account from ChatGPT)
```

## Summary: What You Need


| Item                                        | Required?               | Cost                     | Notes                                     |
| ------------------------------------------- | ----------------------- | ------------------------ | ----------------------------------------- |
| **OpenClaw software**                       | Yes                     | Free                     | Open source, always free                  |
| **Docker Desktop** (if using Docker setup)  | Yes                     | Free                     | Free for personal use                     |
| **AI Provider API key**                     | Yes, pick ONE           | Free to $5/month typical | See options above                         |
| **AWS account** (only if using cloud setup) | Only for AWS            | ~$5-15/month             | Not needed for Docker setup               |
| **Git** (version control)                   | Yes                     | Free                     | Usually pre-installed on Mac              |
| **Node.js** (only for AWS direct install)   | Only for AWS            | Free                     | Docker setup doesn't need this separately |
| **A web browser**                           | Yes                     | Free                     | Chrome, Firefox, Safari -- anything works |
| **Terminal/PowerShell**                     | Yes (for initial setup) | Free                     | Built into your computer                  |


---

# 6. Free vs Paid: What Do You Actually Get?

This is the question everyone asks: *"If there's a free version, why would I ever pay?"*

Great question. Here's the honest, complete answer.

## The AI Provider: Free Tier vs Paid Tier

### What FREE Gets You


| Feature                     | Google Gemini Free               | OpenRouter Free                     | Anthropic $5 Credit           | OpenAI $5 Credit              |
| --------------------------- | -------------------------------- | ----------------------------------- | ----------------------------- | ----------------------------- |
| **Can you use OpenClaw?**   | Yes, fully                       | Yes, fully                          | Yes, fully                    | Yes, fully                    |
| **Quality of AI responses** | Excellent (Gemini 2.5 Pro)       | Good to Excellent (varies by model) | Excellent (Claude Sonnet)     | Excellent (GPT-4o)            |
| **Speed limit**             | 15 requests/min                  | 20 requests/min                     | No hard limit (soft throttle) | No hard limit (soft throttle) |
| **Daily limit**             | ~1,000 requests                  | ~200 requests                       | Until credits run out         | Until credits run out         |
| **Credit card needed?**     | No                               | No                                  | No                            | No                            |
| **Credits expire?**         | Never (it's a tier, not credits) | Never (it's a tier, not credits)    | Never                         | After 3 months                |
| **Enough for a hackathon?** | Yes, easily                      | Tight but possible                  | Yes                           | Yes                           |


### What PAID Gets You (That Free Doesn't)


| Benefit                        | What It Means in Practice                                                                                                                                                              |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Higher rate limits**         | You can send more requests per minute. With free tiers, if you're working fast, you might hit a wall that says "slow down, try again in 60 seconds." Paid tiers rarely hit this.       |
| **Priority access**            | When lots of people are using the AI at once, free users may experience slower responses. Paid users get priority -- like a fast pass at a theme park.                                 |
| **No daily caps**              | Free tiers have daily limits. Paid tiers let you use as much as you want (you just pay for what you use).                                                                              |
| **Access to top models**       | Some cutting-edge models are paid-only. For example, OpenAI's o3 reasoning model requires a paid API account.                                                                          |
| **Better privacy guarantees**  | Google's free Gemini tier may use your data to improve their products. Their *paid* tier explicitly does not. Anthropic and OpenAI don't use API data for training regardless of tier. |
| **Longer conversations**       | Some free tiers reduce the context window (how much the AI "remembers" in one conversation). Paid tiers give you the full memory.                                                      |
| **Batch processing discounts** | Anthropic offers 50% off for batch jobs and 90% off for repeated content (prompt caching). Only available on paid tier.                                                                |


### The Honest Truth About Free vs Paid

**For a one-day hackathon:** Free is completely sufficient. Google Gemini's free tier gives you 1,000 requests/day with their best model. That's more than enough.

**For regular weekly use:** You'll likely spend $5-15/month. That's less than a Netflix subscription for a personal AI assistant.

**For heavy daily use:** Budget $30-50/month. This is power-user territory -- running automated agents, processing large documents, long coding sessions.

### Cost Reality Check: What Does a Typical Session Cost?

Let's say you sit down for a 2-hour session with OpenClaw. Here's roughly what it costs:


| Activity                            | Approximate Cost (Claude Sonnet) | Approximate Cost (GPT-4o-mini) | Approximate Cost (Gemini Free) |
| ----------------------------------- | -------------------------------- | ------------------------------ | ------------------------------ |
| Ask 20 questions with short answers | ~$0.15                           | ~$0.01                         | $0.00                          |
| Ask it to write 5 pages of content  | ~$0.50                           | ~$0.05                         | $0.00                          |
| Have it analyze a 10-page document  | ~$0.30                           | ~$0.03                         | $0.00                          |
| Full 2-hour working session         | ~$1.00 - $3.00                   | ~$0.10 - $0.50                 | $0.00                          |


**You will not accidentally spend $100.** At these prices, even if you used Claude Sonnet heavily for a full month, you'd be in the $15-30 range. Most API providers also let you set spending limits so you'll never go over a budget you choose.

## Docker vs AWS: Free vs Paid


| Component                   | Docker               | AWS                         |
| --------------------------- | -------------------- | --------------------------- |
| **The software (OpenClaw)** | Free                 | Free                        |
| **The infrastructure**      | Free (your laptop)   | ~$5-15/month (EC2 instance) |
| **The AI model**            | Same cost either way | Same cost either way        |
| **Total for hackathon**     | $0 - $5              | $5 - $15                    |


**Bottom line:** Docker + Google Gemini free tier = **$0 total.** You can try everything without spending a single dollar.

---

# 7. Do I HAVE to Use the Terminal?

Short answer: **For the initial setup, yes -- a little bit.** But there are ways to minimize it, and after setup, you can use visual interfaces for everything.

Let's break this down honestly.

## Why OpenClaw Needs the Terminal (Initially)

OpenClaw is a developer tool. Like most developer tools, its installer runs through the terminal (command line). There is currently **no "Download and double-click" installer** like you'd get with Spotify or Zoom.

The Docker setup requires about **6 terminal commands** total. Here they are -- this is everything:

```
git clone https://github.com/openclaw/openclaw.git    # Download OpenClaw
cd openclaw                                            # Go into the folder
echo "GEMINI_API_KEY=your_key_here" > .env             # Save your API key
chmod 600 .env                                         # Lock down the file
export OPENCLAW_SANDBOX=1                              # Enable security mode
./docker-setup.sh                                      # Start everything
```

That's it. Six lines. After that, you use OpenClaw through your **web browser** -- no more terminal needed.

## But I'm Not Comfortable With the Terminal...

That's completely valid. Here are your options, ranked from "least terminal" to "no terminal at all":

### Level 1: Docker Setup + Web Dashboard (Minimal Terminal)

**Terminal needed:** Only for initial setup (the 6 commands above, one time).
**After that:** Everything happens in your browser at `http://127.0.0.1:18789`.

The OpenClaw Gateway provides a **web dashboard** where you can:

- Chat with the AI
- Manage your agents
- See conversation history
- Monitor status

This is the approach in your hackathon setup guide. Once it's running, it genuinely feels like using a website.

**Comfort tip:** You can have someone help you with the 6 setup commands during the hackathon. After that, you're independent.

### Level 2: OpenClaw Mission Control (Community GUI)

**What it is:** A beautiful visual dashboard built by the community specifically for people who don't want to live in the terminal.

**What you see:** A web page at `http://localhost:3333` with:

- Agent status cards (green = running, red = stopped)
- Gateway health monitor
- Start/stop buttons (no commands needed)
- Logs viewer with search
- System resource usage (CPU, memory)

**How to add it** (one extra terminal command during setup):

```
docker run -d -p 3333:3333 --name mission-control openclaw/mission-control
```

After this, you manage OpenClaw by clicking buttons in your browser. Want to restart? Click the restart button. Want to check logs? Click the logs tab.

### Level 3: One-Click Cloud Hosting (Minimal Terminal)

If even 6 terminal commands feel like too much, some cloud providers offer **one-click OpenClaw deployment**:


| Provider                 | How It Works                                                                      | Cost      | Terminal Needed?                      |
| ------------------------ | --------------------------------------------------------------------------------- | --------- | ------------------------------------- |
| **DigitalOcean 1-Click** | Click a button on their website, OpenClaw deploys on a cloud server automatically | ~$6/month | Almost none -- mostly web dashboard   |
| **xCloud Hosting**       | Managed OpenClaw with pre-configured Telegram/WhatsApp                            | Varies    | No -- fully managed through web panel |


These services handle the Docker, the server, the security -- everything. You just configure your API key through their web interface.

**Trade-off:** You're trusting a third party with your setup, and it costs money monthly.

### Level 4: Managed Alternatives (Zero Terminal, Zero Setup)

If the terminal is a complete dealbreaker and you want an experience like **Lovable** (open browser, start working), these alternatives provide similar AI agent functionality with zero technical setup:


| Alternative                    | What It Is                                                | Setup                 | Cost                   | How It Compares to OpenClaw                                           |
| ------------------------------ | --------------------------------------------------------- | --------------------- | ---------------------- | --------------------------------------------------------------------- |
| **Kimi Claw** (by Moonshot AI) | OpenClaw running inside a managed web interface           | Open browser, sign in | Free tier available    | Same OpenClaw tech, but you don't manage anything                     |
| **Lindy AI**                   | Visual drag-and-drop AI agent builder                     | Open browser, sign in | Free tier + paid plans | Different tech, but similar result -- AI agents that do tasks for you |
| **Cats and Claws**             | Visual cloud interface with Kanban dashboard for OpenClaw | Open browser, sign in | Paid                   | OpenClaw with a Lovable-like visual layer on top                      |


**The honest trade-off with managed services:**


| You Get                                    | You Give Up                                       |
| ------------------------------------------ | ------------------------------------------------- |
| Zero terminal commands                     | Your data goes through their servers              |
| Beautiful visual interface                 | Less control over security configuration          |
| Someone else handles updates & maintenance | Monthly subscription costs                        |
| Works from any device immediately          | Dependency on a company staying in business       |
| Support when things break                  | Your conversations may be stored on their servers |


## The "Lovable vs OpenClaw" Comparison

Since you mentioned people are comfortable with Lovable, here's a direct comparison:


| Aspect                        | Lovable                                         | OpenClaw                                                              |
| ----------------------------- | ----------------------------------------------- | --------------------------------------------------------------------- |
| **What it does**              | Builds web apps/websites from text descriptions | Automates tasks, answers questions, runs agents across your chat apps |
| **Open a browser and start?** | Yes                                             | No (setup required first)                                             |
| **Terminal required?**        | Never                                           | Yes, for initial setup                                                |
| **Where data lives**          | Lovable's cloud servers                         | Your machine (Docker) or your cloud server (AWS)                      |
| **Privacy**                   | Lovable sees everything you build               | You control everything (especially with Docker)                       |
| **Price**                     | Subscription ($0-$50/month)                     | Free software + API costs ($0-$15/month)                              |
| **Best for**                  | Building websites and apps visually             | Personal AI assistant, automation, coding help                        |


**They solve different problems.** Lovable is for building apps. OpenClaw is for having a personal AI assistant. They're complementary, not competitors.

## Our Recommendation for the Hackathon

**Use the Docker setup with a helper for the initial 6 commands.** Here's why:

1. **Someone at the hackathon can pair with you** for the 5-minute terminal portion. After that, you're on your own with a browser.
2. **Your data stays on YOUR machine.** Managed services can't guarantee this.
3. **It's free.** No subscriptions, no credit card for the hosting.
4. **Once running, it's just a website.** The dashboard at `127.0.0.1:18789` looks and feels like any other web app.

If the terminal is truly a non-starter, use **Kimi Claw** (web-based, free tier) to get started immediately, and graduate to your own Docker setup when you're ready.

---

# 8. What Is Docker? (And Why Should I Care?)

## The Simple Explanation

Imagine you're baking a cake. You could bake it in your own kitchen, using your own oven, with your own ingredients. Nobody else is involved. When you're done, you clean up and your kitchen goes back to normal.

**Docker is your own private kitchen on your computer.**

It creates a sealed-off space (called a "container") where OpenClaw runs. This container:

- Has its own mini operating system inside it
- Cannot access your personal files, photos, or passwords
- Cannot install anything on your real computer
- Disappears completely when you shut it down

## Why Docker Exists

In the old days, installing software was messy. It would scatter files all over your computer, change settings, and sometimes break other programs. Docker was invented to solve this. It packages everything an app needs into one neat box that keeps to itself.

## What Docker Looks Like in Practice

When you install Docker Desktop, you get a simple application with a green/red indicator:

- **Green whale icon** = Docker is running, you're good to go
- **Red/gray** = Docker is stopped, containers aren't active

You never have to look inside the container. You just start it and use OpenClaw through your web browser at a local address (`127.0.0.1` -- which literally means "this computer, right here").

## Docker: The Security Angle

Here's what makes Docker particularly good for someone who cares about security:


| Security Feature            | What It Means For You                                                                                                              |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Runs in a sandbox**       | OpenClaw is in a locked room. It cannot peek at your files, emails, or browser history.                                            |
| **Read-only filesystem**    | The container can't permanently change anything -- not even inside itself.                                                         |
| **Non-root user**           | The software runs with minimal permissions, like a guest account on your laptop.                                                   |
| **Localhost-only binding**  | The dashboard is only accessible from YOUR computer. Nobody on your Wi-Fi, your neighbor, or a hacker across the world can see it. |
| **Disappears on cleanup**   | One command (`docker compose down -v`) and it's like it was never there. No leftover files. No traces.                             |
| **No cloud account needed** | You don't create any online account. No username. No password stored somewhere.                                                    |


## What Docker Does NOT Do

Let's be clear about what Docker is **not**:

- It is **not** a virus or malware
- It does **not** send your data anywhere
- It does **not** need your personal information
- It does **not** run when you close it
- It does **not** have access to your webcam, microphone, or location

---

# 9. What Is AWS? (The Cloud, Demystified)

## The Simple Explanation

Going back to our baking analogy: AWS is like **renting a professional kitchen** in a building downtown. You don't own it -- Amazon does -- but you get your own private room with your own key. You can leave, come back the next day, and your cake is still in the oven.

**AWS EC2** (what the OpenClaw guide uses) gives you a **virtual computer** running in Amazon's data center. It's a real computer -- with a processor, memory, and storage -- but it's located in an Amazon building, not on your desk.

## Why People Use AWS

- Your laptop can turn off, lose Wi-Fi, or run out of battery. AWS stays on 24/7.
- If you want OpenClaw running continuously (e.g., connected to a Telegram bot that answers messages while you sleep), it needs to be "always on."
- AWS is how most of the internet works. Netflix, Airbnb, and thousands of companies run on AWS.

## AWS: The Security Angle


| Security Feature               | What It Means For You                                                                                     |
| ------------------------------ | --------------------------------------------------------------------------------------------------------- |
| **Your own virtual machine**   | Your EC2 server is isolated from other customers. Amazon can't see inside it.                             |
| **SSH key authentication**     | You access your server with a key file (like a digital key to a padlock). No password to guess.           |
| **Firewall (Security Groups)** | You control exactly which internet addresses can connect to your server.                                  |
| **Physical security**          | Amazon's data centers have 24/7 guards, biometric access, and surveillance. Your data is physically safe. |
| **Encryption in transit**      | Communication between you and the server is encrypted (scrambled so nobody can eavesdrop).                |


## What AWS Requires That Docker Doesn't

Here's the honest part -- AWS asks for more from you:


| Requirement                         | Why It Might Concern You                                                                                         |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **AWS account with credit card**    | Amazon charges ~$5-10/month. You must provide payment info.                                                      |
| **A `.pem` key file**               | This is like a house key to your server. If someone gets it, they can access your server. You MUST keep it safe. |
| **SSH (command-line access)**       | You manage the server through typed commands, not a visual interface.                                            |
| **You're responsible for updates**  | Unlike your phone that auto-updates, you must manually keep the server secure.                                   |
| **Data lives on Amazon's hardware** | Your files are on Amazon's physical hard drives, not yours.                                                      |


---

# 10. Docker vs AWS: The Full Comparison

## Comparison 1: Security & Privacy

### Why Docker Is Better for Security & Privacy

**Reason 1: Your data never leaves your physical possession.**

With Docker, everything runs on your laptop. Your API key, your conversations with the AI, your project files -- all of it stays on the machine sitting in front of you. There is no network connection carrying your data to a remote server. There is no company storing your information on hardware you cannot see or touch. If you close your laptop lid, it all stops. If you delete the container, it all disappears.

This matters because the number one security principle is: **data you control physically is data you control completely.** No matter how good Amazon's security is, your personal laptop behind your home Wi-Fi with Docker's sandbox is a smaller attack surface. In security, "smaller" means "safer."

For a beginner, this also eliminates an entire category of worry. You don't have to think about:

- "Did I lock down my server's firewall?"
- "Is my SSH key stored safely?"
- "Is someone trying to break into my cloud machine?"
- "Am I accidentally paying for something I forgot to turn off?"

With Docker, none of those questions exist.

**Reason 2: Zero account exposure.**

Docker Desktop is a free download. You install it like any other app. You don't create a Docker account to use it for OpenClaw. You don't enter your email, phone number, or credit card. The only sensitive thing you handle is your AI provider API key (which you'd need in both setups anyway).

With AWS, you create an account tied to your real identity and credit card. That's one more account that could be:

- Subject to a data breach
- Accidentally charged if you forget to shut down your server
- Targeted by phishing emails pretending to be Amazon

For someone who is security-conscious and new to this, fewer accounts = fewer risks.

---

### Why AWS Is Better for Security & Privacy

**Reason 1: Separation from your personal machine.**

Here's the flip side: when OpenClaw runs inside Docker on your laptop, it's still **on your laptop.** If your laptop gets stolen, has malware, or someone accesses it while unlocked, the Docker container is accessible too.

With AWS, your OpenClaw setup is on a completely separate machine in a data center. Your laptop could be lost, damaged, or compromised, and your OpenClaw server remains untouched and unaffected. The only way to access it is with the `.pem` key file -- which you can store in a password manager or encrypted USB drive, separate from the laptop.

This is the same principle banks use: they don't keep your money in your house. They keep it in a vault somewhere else, accessible only with your credentials.

**Reason 2: Professional-grade infrastructure security.**

Amazon employs thousands of security engineers. Their data centers meet compliance standards like SOC 2, ISO 27001, and HIPAA. They have:

- Automatic DDoS (attack) protection
- Network monitoring 24/7
- Hardware encryption
- Redundant power and backups

Your home laptop has... your antivirus software and your Wi-Fi password. For long-running, always-on deployments, AWS's professional security infrastructure is genuinely stronger than most home setups.

---

## Comparison 2: Cost

### Why Docker Is Better for Cost

**Reason 1: It's completely free.**

Docker Desktop is free for personal use. Running OpenClaw in a container uses your laptop's existing CPU and memory -- resources you've already paid for when you bought the computer. The only cost is your AI provider API key (a few dollars for typical usage), which you'd pay regardless of Docker or AWS.

There are no surprise bills. No "I forgot to turn off my server and got charged $50." No credit card authorization holds. No billing dashboards to monitor.

**Reason 2: No hidden costs or billing surprises.**

AWS billing is notoriously confusing, even for experienced engineers. Costs come from:

- EC2 instance hours (~$0.02/hour for t3.small = ~$15/month if always on)
- Data transfer (small, but it adds up)
- Storage (EBS volumes)
- Potential extra charges for static IPs, snapshots, etc.

For someone new to cloud computing, the risk of accidentally leaving a server running (or spinning up additional resources unknowingly) is real. AWS's "pay-as-you-go" model means the meter is always running when your server is on.

---

### Why AWS Is Better for Cost

**Reason 1: Your laptop's resources are freed up.**

Running OpenClaw in Docker uses your laptop's CPU and RAM. On a machine with 8GB of RAM, giving 4GB to Docker means everything else (your browser, email, video calls) shares the remaining 4GB. Your laptop may feel slower, its fan may spin louder, and battery life will decrease.

AWS offloads this work to a dedicated machine. Your laptop stays fast and responsive. If your laptop is older or has limited specs, this isn't just about cost -- it's about whether Docker can run smoothly at all.

**Reason 2: 24/7 operation without personal hardware wear.**

If you need OpenClaw running continuously (e.g., a Telegram bot responding to messages), Docker means your laptop must stay open, plugged in, and connected to Wi-Fi permanently. That wears out your battery, screen, and SSD. Over months, that "free" Docker setup is costing you laptop lifespan. AWS keeps the wear off your personal device.

---

## Comparison 3: Ease of Use

### Why Docker Is Better for Ease of Use

**Reason 1: Fewer steps, less can go wrong.**

Let's count the steps:


| Docker Setup              | AWS Setup                       |
| ------------------------- | ------------------------------- |
| 1. Install Docker Desktop | 1. Create AWS account           |
| 2. Get API key            | 2. Launch EC2 instance          |
| 3. Open Terminal          | 3. Configure security group     |
| 4. Clone repository       | 4. Download SSH key             |
| 5. Create `.env` file     | 5. Connect via SSH              |
| 6. Run setup script       | 6. Install system updates       |
| 7. Open browser           | 7. Install Node.js              |
|                           | 8. Install OpenClaw             |
|                           | 9. Fix PATH variable            |
|                           | 10. Run onboarding              |
|                           | 11. Complete OAuth              |
|                           | 12. Install PM2 process manager |
|                           | 13. Configure Telegram bot      |


Docker: **7 steps.** AWS: **13 steps** (and several involve typing precise commands into a remote terminal).

**Reason 2: Everything is visual.**

Docker Desktop has a graphical interface. You can see your containers, start/stop them with buttons, and check logs visually. The OpenClaw dashboard opens in your regular browser. It feels like using a normal app.

AWS requires SSH (a command-line connection to a remote server). There's no visual interface for the server itself. If you mistype a command, the error messages can be cryptic. For someone who's never used a terminal before, this is a significant barrier.

---

### Why AWS Is Better for Ease of Use

**Reason 1: Always available -- no daily startup routine.**

With Docker, every time you want to use OpenClaw, you need to:

1. Open Docker Desktop
2. Wait for it to start (~30 seconds)
3. Open Terminal
4. Run `docker compose up`
5. Open browser to the dashboard

With AWS + Telegram, you just... open Telegram on your phone and type. The server is already running. This is like the difference between cooking at home (setup, cook, cleanup) vs. texting your order to a restaurant. If you plan to use OpenClaw frequently, "always ready" is genuinely easier.

**Reason 2: Accessible from any device.**

Docker locks you to the laptop where it's installed. AWS with Telegram means you can interact with OpenClaw from your phone, tablet, work computer, or any device with Telegram. You're not tied to one machine.

---

## Comparison 4: Reliability & Performance

### Why Docker Is Better for Reliability

**Reason 1: No internet dependency for local processing.**

Docker runs on your machine. If your Wi-Fi goes down, Docker still runs. (The AI model calls need internet, but your local setup, files, and configurations are all accessible offline.) With AWS, if your internet drops, you lose connection to your server entirely.

**Reason 2: Predictable behavior.**

Your laptop's specs don't change. Docker will perform the same way every time. AWS performance can vary slightly based on the shared infrastructure, and you may encounter occasional network latency between your laptop and the data center.

---

### Why AWS Is Better for Reliability

**Reason 1: Doesn't depend on your laptop's health.**

If your laptop crashes, runs out of battery, needs a restart for updates, or the screen breaks -- your Docker setup goes down with it. AWS keeps running independently. For anything that needs to stay available (like a bot or continuous monitoring), AWS is inherently more reliable.

**Reason 2: Designed for uptime.**

AWS data centers have redundant power supplies, backup generators, multiple internet connections, and hardware that's monitored 24/7. Your laptop has one power cable, one battery, and one Wi-Fi connection. AWS infrastructure is engineered for 99.99% uptime. Your laptop... is not.

---

## Comparison 5: Cleanup & Exit Strategy

### Why Docker Is Better for Cleanup

**Reason 1: Total erasure in seconds.**

```
docker compose down -v     # Stop everything
docker rmi openclaw:local  # Delete the image
```

Two commands and OpenClaw is completely gone. No files scattered across your system. No accounts to delete. No servers running somewhere charging your card. No SSH keys floating around. It's the digital equivalent of packing up a tent -- when you leave, there's no trace you were ever there.

**Reason 2: No ongoing obligations.**

With Docker, when you're done, you're done. There's nothing to cancel, no subscription to remember, no server to "terminate." You don't have to log into a cloud console 3 months later and wonder "wait, is that thing still running?"

---

### Why AWS Is Better for Cleanup

**Reason 1: Your local machine stays untouched.**

With Docker, the container is gone but Docker Desktop itself is still installed on your laptop (~2-4GB). The git clone is still there. The `.env` file with your API key needs to be securely deleted. Your laptop was the host, so cleanup involves your personal machine.

With AWS, everything lived on a remote server. You click "Terminate Instance" in the AWS console, and the virtual machine is destroyed. Your laptop never had any of it. Nothing to find, nothing to delete locally (except the `.pem` key file).

**Reason 2: Instant, complete destruction.**

When you terminate an EC2 instance, AWS physically wipes the storage. It's not "moved to trash" -- it's gone. The IP address is recycled, the SSH key becomes useless, and the server ceases to exist. This is actually more thorough than deleting files on your laptop, where "deleted" files can sometimes be recovered with special software.

---

# 11. Security Deep Dive: Where Does My Data Go?

This is the section that matters most if you're security-conscious. Let's trace exactly where your data flows in each setup.

## Docker: Data Flow

```
┌─────────────────────────────────────────────────┐
│               YOUR LAPTOP                       │
│                                                 │
│   ┌─────────────────────────────────────────┐   │
│   │         DOCKER CONTAINER (sandbox)      │   │
│   │                                         │   │
│   │   OpenClaw ────► AI Provider API        │───┼──► Internet (encrypted)
│   │      │            (Claude/GPT/Gemini)   │   │     ONLY for AI calls
│   │      │                                  │   │
│   │   Your project files                    │   │
│   │   (only files you explicitly share)     │   │
│   │                                         │   │
│   └─────────────────────────────────────────┘   │
│                                                 │
│   Your photos, emails, banking ← NOT ACCESSIBLE │
│                                                 │
└─────────────────────────────────────────────────┘
```

**What goes to the internet:** Only your prompts/questions go to the AI provider (Claude, GPT, etc.) via encrypted HTTPS. Nothing else.

**What stays local:** Everything else. Your files, configuration, conversation history, API key -- all on your laptop, inside the container.

**Who can see it:** Only you, sitting at your laptop, logged into your user account.

## AWS: Data Flow

```
┌──────────────┐          Encrypted SSH          ┌─────────────────────┐
│  YOUR LAPTOP │ ◄──────────────────────────────► │   AWS EC2 SERVER    │
│              │    (you type commands here)       │                     │
│  - .pem key  │                                  │  OpenClaw running   │
│  - Browser   │                                  │  Your project files │
│              │                                  │  API key stored     │
└──────────────┘                                  │       │             │
                                                  │       ▼             │
                                                  │  AI Provider API ───┼──► Internet
                                                  │  (Claude/GPT)       │    (encrypted)
                                                  │       │             │
                                                  │       ▼             │
                                                  │  Telegram Bot ──────┼──► Telegram servers
                                                  │                     │    (encrypted)
                                                  └─────────────────────┘
                                                      Located in an
                                                    Amazon data center
```

**What goes to the internet:** Your prompts go to the AI provider AND potentially to Telegram (if configured). SSH traffic goes between your laptop and AWS.

**What's stored remotely:** Your project files, API key, OpenClaw configuration, and conversation history all live on AWS hardware.

**Who can see it:** You (via SSH), and theoretically, someone who obtains your `.pem` key file or gains access to your AWS account.

## The API Key: Your Most Sensitive Piece

In **both** setups, you'll create an API key. This is like a password that lets OpenClaw talk to the AI model. Here's how to protect it:


| Practice                 | Docker                                 | AWS                    |
| ------------------------ | -------------------------------------- | ---------------------- |
| **Store in `.env` file** | Yes, on your laptop                    | Yes, on the server     |
| **Set file permissions** | `chmod 600 .env` (only you can read)   | Same command on server |
| **Never commit to Git**  | Add `.env` to `.gitignore`             | Same                   |
| **Revoke when done**     | Go to provider website, delete the key | Same                   |
| **Rotate periodically**  | Generate new key, update `.env`        | Same                   |


---

# 12. Which One Should I Choose?

## Choose Docker If...

- This is your first time using AI tools
- You're trying this for a hackathon or short-term project
- Privacy and data control are your top priorities
- You don't want to create cloud accounts or enter credit cards
- You want the easiest cleanup when you're done
- You're comfortable with your laptop being on while using it
- You prefer "nothing leaves my machine"

## Choose AWS If...

- You want OpenClaw running 24/7 without your laptop being open
- You're connecting it to Telegram or other messaging platforms
- You plan to use it long-term beyond a hackathon
- You want to access it from multiple devices (phone, tablet, etc.)
- You're comfortable with basic command-line operations
- You're okay with ~$5-10/month in costs
- You understand the responsibility of managing a cloud server

## The Honest Recommendation for Beginners

**Start with Docker.** Here's why:

1. **Lower stakes.** If something goes wrong, the worst case is you delete the container and try again. There's nothing to "break" and no bills to worry about.
2. **Build confidence first.** Docker teaches you the core concepts (containers, terminals, API keys) in a safe environment. Once comfortable, AWS will feel much less intimidating.
3. **Security by default.** Docker's localhost-only setup means you literally cannot expose it to the internet accidentally. With AWS, a misconfigured firewall rule can make your server visible to the world.
4. **Perfect for a hackathon.** You'll set it up, use it for the event, and cleanly remove it afterward. That's exactly what Docker was designed for.

---

# 13. Glossary: Tech Terms in Plain English


| Term                      | What It Actually Means                                                                                                                                                                               |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Docker**                | Software that creates isolated "containers" on your computer -- like sealed rooms where apps run without affecting your stuff.                                                                       |
| **Container**             | A lightweight, sealed-off space where an app runs. Think of it as an app in a bubble.                                                                                                                |
| **Docker Desktop**        | The app you install on your Mac/Windows to manage containers. Has a nice visual interface.                                                                                                           |
| **Docker Compose**        | A tool that starts up multiple containers at once using a recipe file (`docker-compose.yml`).                                                                                                        |
| **AWS**                   | Amazon Web Services -- Amazon's cloud computing platform. Basically, renting computers from Amazon.                                                                                                  |
| **EC2**                   | Elastic Compute Cloud -- a virtual computer you rent from AWS.                                                                                                                                       |
| **SSH**                   | Secure Shell -- a way to securely connect to and control a remote computer using typed commands.                                                                                                     |
| `**.pem` file**           | A digital key file that proves you're authorized to access your AWS server. Treat it like a house key.                                                                                               |
| `**.env` file**           | A simple text file where you store secret settings (like API keys) so they're not hard-coded in your project.                                                                                        |
| **Terminal**              | The text-based interface where you type commands. Mac: Terminal app. Windows: PowerShell.                                                                                                            |
| **Localhost / 127.0.0.1** | An address that means "this computer." When you visit `127.0.0.1`, you're talking to your own machine, not the internet.                                                                             |
| **Port**                  | A numbered doorway on a computer. OpenClaw uses port `18789` -- like apartment number 18789 in your computer's building.                                                                             |
| **Sandbox**               | A restricted environment where software can run but can't affect the rest of your system. Like a playpen for apps.                                                                                   |
| **Firewall**              | A security guard that controls which network traffic can enter and leave a computer.                                                                                                                 |
| **Security Group**        | AWS's version of a firewall -- rules that say who can connect to your server and how.                                                                                                                |
| **Git / Clone**           | Git tracks changes to code. "Cloning" means downloading a copy of a project to your computer.                                                                                                        |
| **Node.js**               | A platform that lets JavaScript (a programming language) run outside of a web browser.                                                                                                               |
| **PM2**                   | A process manager that keeps programs running even after you disconnect from the server. Like a babysitter for your app.                                                                             |
| **OAuth**                 | A way to log in to one service using your account from another (e.g., "Sign in with Google"). Avoids sharing your password.                                                                          |
| **Encryption**            | Scrambling data so only the intended recipient can read it. Like sending a letter in a locked box where only you and the recipient have keys.                                                        |
| **DDoS**                  | Distributed Denial of Service -- an attack that floods a server with fake traffic to crash it.                                                                                                       |
| **API**                   | Application Programming Interface -- a way for two pieces of software to talk to each other. OpenClaw uses APIs to talk to AI models.                                                                |
| **API Key**               | A secret code (like `sk-ant-api03-xYz...`) that proves you're allowed to use an AI service. Like a library card for AI.                                                                              |
| **Token**                 | The unit AI companies use to measure text. Roughly 1 token = 0.75 words. When they say "$3 per million tokens," they mean per ~750,000 words.                                                        |
| **Free Tier**             | A limited-but-functional version of a paid service that costs $0. Usually has rate limits (how fast you can use it) and daily caps.                                                                  |
| **Rate Limit**            | A speed limit on how many requests you can make per minute. Like a "15 items or less" checkout lane.                                                                                                 |
| **Context Window**        | How much the AI can "remember" in one conversation. A 1 million token context window means it can consider ~750,000 words at once.                                                                   |
| **GUI**                   | Graphical User Interface -- the visual version of software with buttons, menus, and windows (as opposed to typing commands in a terminal).                                                           |
| **CLI**                   | Command Line Interface -- the text-based version of software where you type commands. The opposite of a GUI.                                                                                         |
| **Open Source**           | Software whose code is publicly visible. Anyone can inspect it, which means security issues are harder to hide. OpenClaw is open source.                                                             |
| **Managed Service**       | When a company runs and maintains software for you (like Kimi Claw or Lindy AI). You pay them so you don't have to do the technical work yourself.                                                   |
| **OAuth**                 | A way to log in to one service using your account from another (e.g., "Sign in with Google"). Avoids sharing your actual password.                                                                   |
| **Lovable**               | A popular browser-based AI app builder where you describe what you want and it builds it visually. No terminal needed. Different from OpenClaw (which is an AI assistant/agent, not an app builder). |
| **Ollama**                | Free software that runs AI models locally on your own computer. No internet needed, maximum privacy. Requires decent hardware (8GB+ RAM). |
| **Claude Code**           | A terminal-based coding assistant from Anthropic. Different from OpenClaw -- it helps with programming, not personal automation. |
| **Cursor**                | An AI-powered code editor (like a smart version of Microsoft Word but for programmers). Not needed for OpenClaw. |
| **GitHub Copilot**        | An AI that suggests code as you type, made by GitHub/Microsoft. A programming tool, not related to OpenClaw. |
| **Agent**                 | An AI that doesn't just answer questions but can actually *do things* -- send messages, manage files, browse the web, run commands. OpenClaw is an agent. |
| **Gateway**               | OpenClaw's core service that runs on your machine and connects your messaging apps to the AI brain. Think of it as the "engine" of OpenClaw. |


---

## Final Thought

Technology is not inherently dangerous -- but it does reward the informed. By reading this guide, you've already done something most people skip: **understanding what's happening before diving in.**

Whether you choose Docker or AWS, you're making a deliberate, informed choice. That's the best security practice of all.

---

*Created for the March 14, 2026 Hackathon*
*Audience: Women new to AI tools who prioritize security and privacy*