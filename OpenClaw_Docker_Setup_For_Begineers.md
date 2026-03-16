# OpenClaw Hackathon Setup Guide

## Overview

**OpenClaw** is an open-source coding assistant that runs in your browser using AI. Think of it like having a smart helper that can write and understand code — and it all runs on **your own laptop** inside a sealed container called **Docker**.

This guide walks you through installing Docker, getting an AI **API key**, and launching OpenClaw. It's written for people who have **never touched a terminal before** — so don't worry, we'll explain everything along the way.

**What you need:** Mac or Windows 10/11, internet connection, ~20 minutes, a credit/debit card for the API key (typically costs a few dollars).

---

## Prerequisites & System Requirements

Before you begin, make sure your machine meets these minimums:

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| **OS** | macOS 12+ / Windows 10 (21H2+) | macOS 13+ / Windows 11 |
| **CPU** | 2 cores | 4+ cores |
| **RAM** | 4 GB free | 8 GB free |
| **Disk** | 10 GB free | 20 GB free |
| **Docker Desktop** | 4.20+ (Engine 25+) | Latest stable |
| **Docker Compose** | v2 (bundled with Docker Desktop) | Latest |
| **Git** | 2.30+ | Latest |

> **Apple Silicon (M1/M2/M3/M4):** Fully supported. Docker Desktop runs natively on ARM — just download the "Apple Silicon" version in Step 1.

> **Windows + WSL 2:** Docker Desktop on Windows requires **WSL 2** (Windows Subsystem for Linux). If Docker prompts you to install it, follow the on-screen instructions and restart. If your company locks down WSL, ask IT to enable it or use a personal machine.

> **VPN / Corporate Proxy / Firewall Warning:** If you're on a corporate or school network, VPNs, proxies, and firewalls can block Docker image pulls and container networking. Signs: `timeout`, `TLS handshake error`, or `connection refused` during build. **Fix:** Disconnect from the VPN, use a personal hotspot, or ask IT to whitelist `registry-1.docker.io`, `ghcr.io`, and `production.cloudflare.docker.com`.

---

## Important: Security Awareness — Read This First

> **Be transparent with yourself: this setup has real security considerations.**
>
> We've built this guide with hardening steps to **mitigate and minimize risk** — but no setup is perfectly safe. After you're up and running, **how you use OpenClaw can still introduce security challenges**. A guide can protect the setup, but it can't protect every decision you make afterward.
>
> **Operate with caution and a safety-first mindset at all times.** Don't assume everything is safe just because you followed a guide. Stay alert, keep your guard up, and treat your API keys and data like you'd treat your bank password.
>
> This guide addresses three pillars of security:
>
> - **Docker security hardening** — locking down the container so it can't do more than it needs to
> - **API key protection** — keeping your secret keys out of the wrong hands
> - **Data privacy controls** — making sure your work stays on your machine
>
> The steps below will walk you through each of these, but **you** are the last line of defense. When in doubt, ask a mentor.

---

## Terminal Basics for Absolute Beginners

Before we dive into the steps, let's cover the tool you'll be using the most: the **terminal** (also called the **command line** or **CLI**).

### What is a terminal?

A terminal is just a way to **talk to your computer by typing text** instead of clicking icons. You type a command, press **Enter**, and the computer does something and replies with text. That's it. Think of it like **texting your computer** instead of pointing and clicking.

### How to open the terminal

- **Mac:** Press **Command + Space** (this opens Spotlight search), type **Terminal**, and press **Enter**.
- **Windows:** Press the **Windows key** on your keyboard, type **PowerShell**, and click **"Windows PowerShell"**.

A window will open with a blinking cursor. That's your terminal. You're ready.

### Essential concepts

| Concept | What it means | Analogy |
|---------|--------------|---------|
| **Command** | A line of text you type and press Enter to execute | Like sending a text message to your computer |
| **Directory / Folder** | A location on your computer where files live | Same as folders in Finder (Mac) or File Explorer (Windows) |
| **`cd`** (change directory) | Moves you into a different folder | Like double-clicking a folder to open it |
| **`~`** (tilde) | Shortcut for your **home folder** (e.g., `/Users/yourname`) | Your personal starting point |
| **Path** | The full address of a file or folder | Like a street address for a file |

### Commands you'll use

| What you want to do | Mac command | Windows (PowerShell) command |
|---------------------|-------------|------------------------------|
| **See where you are** | `pwd` | `cd` (by itself, no arguments) |
| **List files in current folder** | `ls` | `dir` |
| **Move into a folder** | `cd foldername` | `cd foldername` |
| **Go to your home folder** | `cd ~` | `cd ~` |
| **Go up one folder** | `cd ..` | `cd ..` |

### Copy-paste in the terminal

You'll be copy-pasting commands from this guide a lot. Here's how:

- **Mac Terminal:** **Command + V** to paste.
- **Windows PowerShell:** **Right-click** anywhere in the window to paste. (Ctrl+V may also work in newer versions.)

### Don't panic

If something looks wrong — weird text, a wall of errors, a frozen screen — you can **close the terminal window and open a new one**. Nothing will break. Your files are still there. The terminal is just a window; closing it doesn't delete anything.

---

## Step 1: Install Docker Desktop

Docker is like a **sealed box** that runs OpenClaw inside your computer. It keeps things isolated and safe. You need to install it first.

### On Mac

1. Go to **https://www.docker.com/products/docker-desktop/** and click **"Download for Mac"**.
   - **Apple Silicon** = Mac made in 2021 or later (M1/M2/M3/M4 chip). **Intel** = older Macs.

> **Tip:** Not sure which chip you have? Click the **Apple menu** (top-left corner of your screen) > **"About This Mac"** and look at the "Chip" field.

2. Open the downloaded **Docker.dmg** file, drag Docker to Applications, then launch **Docker** from your Applications folder.
3. Approve any permission prompts and **wait** for the whale icon in the menu bar to stop animating (~1-2 min).
4. **Verify it worked.** Open your terminal and type:

```bash
docker --version
```

Press **Enter**.

✅ **What success looks like:** `Docker version 27.5.1, build 9f9e405` (your version number may differ — that's fine).

❌ **If you see `command not found`:** Docker didn't install correctly. Close the terminal, reopen it, and try again. If it still fails, see the Troubleshooting section.

### On Windows

1. Go to **https://www.docker.com/products/docker-desktop/** and click **"Download for Windows"**.
2. Run the installer with default settings. Click **"Close and restart"** when done.
3. After restart, open **Docker Desktop** from the Start menu. Accept the service agreement, skip sign-in.
4. **Wait** until it shows **"Docker Desktop is running"** (~1-2 min).

> **Warning:** If you see a message about **"WSL 2"**, follow the on-screen instructions to install it, restart your computer, and reopen Docker Desktop.

5. **Verify it worked.** Open PowerShell and type:

```powershell
docker --version
```

Press **Enter**.

✅ **What success looks like:** `Docker version 27.5.1, build 9f9e405` (version number may differ).

❌ **If you see an error:** Close PowerShell, reopen it, and try again. If it still fails, see the Troubleshooting section.

---

## Step 2: Get Your API Key

An **API key** is like a **secret password** that lets OpenClaw talk to an AI service. You only need **one** key from **one** provider.

> **Security reminder:** Your API key is linked to your billing account. Treat it like a credit card number — never share it, never paste it in chat or email, never post it publicly.

> **Tip:** Quick comparison:
>
> | Provider | Free Credits | Best For |
> |----------|-------------|----------|
> | **Anthropic (Claude)** | $5 for new accounts | Strong coding and reasoning |
> | **Google (Gemini)** | Generous free tier | Free usage, multimodal |
> | **OpenAI (GPT-4o)** | $5 for new accounts | Wide ecosystem, general purpose |

---

### Option A: Anthropic (Claude)

1. Go to **https://console.anthropic.com/** and **sign up** or **log in**.
2. Click **"API keys"** in the left sidebar.
3. Click **"Create Key"**, name it **hackathon**, click **"Create Key"**.
4. Your key appears (starts with `sk-ant-`). Click the **copy icon** and **save it immediately** — paste it into a temporary note or text file on your computer.

> **Warning:** This is the **only time** the full key is shown. If you lose it, you'll need to create a new one.

5. **Set up billing:** Left sidebar > **Settings** > **Billing** > **Add Payment Method**. Consider setting a **usage limit** (e.g., $10) so you don't get a surprise bill.

> **Tip:** New accounts often get **$5 in free credits**.

---

### Option B: Google (Gemini)

1. Go to **https://aistudio.google.com/** and **sign in** with your Google account.
2. Click **"Get API key"** in the left sidebar.
3. Click **"Create API key"**. If asked to select a project, click **"Create API key in new project"**.
4. Your key appears (starts with `AIzaSy`). Click the **copy icon** and **save it immediately**.

> **Tip:** Gemini has a generous free tier — you likely won't be charged at all. Details at **https://ai.google.dev/pricing**

**Optional billing** (only if you exceed the free tier): Go to **https://console.cloud.google.com/billing** and link a billing account.

---

### Option C: OpenAI (GPT-4o)

1. Go to **https://platform.openai.com/** and **sign up** or **log in**.
2. Click **"API keys"** in the left sidebar, or go directly to **https://platform.openai.com/api-keys**
3. Click **"+ Create new secret key"**, name it **hackathon**, click **"Create secret key"**.
4. Your key appears (starts with `sk-proj-`). Click the **copy button** and **save it immediately**.

> **Warning:** OpenAI will **never show this key again** after you close the pop-up.

5. **Set up billing:** Left sidebar > **Settings** > **Billing** > **Add payment details**. Choose **"Individual"**, add your card, and set an initial credit (e.g., **$10**).

> **Tip:** Set a **monthly budget limit** under Settings > Limits to cap your spending.

---

### Key Reference Table

| Provider | Key Starts With | Environment Variable |
|----------|----------------|---------------------|
| Anthropic | `sk-ant-` | `ANTHROPIC_API_KEY` |
| Google Gemini | `AIzaSy` | `GEMINI_API_KEY` |
| OpenAI | `sk-proj-` | `OPENAI_API_KEY` |

> **Warning:** NEVER share your API key with anyone — not in chat, email, Slack, or anywhere public. Anyone with your key can charge your account.

> **Where to store secrets safely:** Never put API keys in source code, commit messages, or chat. Use the `.env` file (Step 5) and ensure it's in `.gitignore` (Step 5a). For long-term projects beyond this hackathon, consider a secrets manager like 1Password, Bitwarden, or macOS Keychain.

---

## Step 3: Open Your Terminal or CLI

If you closed your terminal from earlier, open it again:

- **Mac:** Press **Command + Space**, type **Terminal**, press **Enter**.
- **Windows:** Press the **Windows key**, type **PowerShell**, click **"Windows PowerShell"**.

✅ **What success looks like:** A window with a blinking cursor, ready for you to type.

---

## Step 4: Clone OpenClaw

"Cloning" means **downloading the project's code** from the internet to your computer using Git.

First, check if **Git** is installed:

```bash
git --version
```

Press **Enter**.

✅ **What success looks like:** Something like `git version 2.39.0`.

❌ **If you see `command not found` or `not recognized`:**
- **Mac:** Type `xcode-select --install` and press **Enter**. Follow the prompts. This may take a few minutes.
- **Windows:** Download and install from **https://git-scm.com/download/win** (use all default settings). **Close PowerShell and reopen it** after installing.

### Clone the Project

Type these commands one at a time, pressing **Enter** after each:

```bash
# Download OpenClaw
git clone https://github.com/openclaw/openclaw.git

# Enter the project folder
cd openclaw
```

✅ **What success looks like:** No errors, and your terminal prompt now shows `openclaw` somewhere in it.

❌ **If you see `Authentication failed` or `Invalid username or token`:** The repo may be private. Follow the steps below to authenticate.

> **Tip:** If the URL doesn't work, ask your hackathon organizer for the correct one.

### If cloning fails: Authenticate with GitHub

The repo may be private. You need a GitHub account and to authenticate your terminal.

**A. Create a GitHub account (skip if you already have one):**

1. Go to **https://github.com/signup**
2. Enter your email, create a password, and choose a username.
3. Complete the verification and click **"Create account"**.
4. Check your email and **verify your account**.
5. **Ask your hackathon organizer to add your GitHub username to the repo** — they need to grant you access before you can clone.

**B. Install the GitHub CLI (`gh`):**

- **Mac:**
```bash
brew install gh
```
If you don't have Homebrew, install it first:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Then run `brew install gh` again.

- **Windows:**
```powershell
winget install --id GitHub.cli
```
**Close and reopen PowerShell** after installing.

**C. Log in to GitHub from your terminal:**

```bash
gh auth login
```

You'll see a series of prompts. Choose these options:
1. **"Where do you use GitHub?"** → select **GitHub.com**
2. **"What is your preferred protocol?"** → select **HTTPS**
3. **"Authenticate Git with your GitHub credentials?"** → select **Yes**
4. **"How would you like to authenticate?"** → select **Login with a web browser**
5. Copy the **one-time code** shown in your terminal.
6. Your browser will open. **Paste the code**, click **"Authorize"**, and confirm.
7. Back in your terminal, you should see **"Logged in as yourusername"**.

✅ **What success looks like:** `✓ Logged in as yourusername`

**D. Try cloning again:**

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
```

> **Tip:** If it still fails, ask your hackathon organizer — they may need to add you to the repo, or provide a direct ZIP download.

---

## Step 5: Set Up Your API Key

You need to create a special file called **.env** inside the `openclaw` folder. This file holds your secret API key so Docker can pass it to OpenClaw.

**Make sure your terminal is in the openclaw folder.** Check by running:

```bash
# Mac
pwd

# Windows (just type cd by itself)
cd
```

✅ **What success looks like:** The output should end with `openclaw`. If not, type `cd ~/openclaw` (Mac) or `cd ~\openclaw` (Windows) and press **Enter**.

Now run **only one** of these commands, matching your provider. **Replace `YOUR_KEY_HERE` with your actual key** (paste it in place of that text):

### On Mac

```bash
# Pick ONE of these:
echo "ANTHROPIC_API_KEY=YOUR_KEY_HERE" > .env    # for Claude
echo "GEMINI_API_KEY=YOUR_KEY_HERE" > .env       # for Gemini
echo "OPENAI_API_KEY=YOUR_KEY_HERE" > .env       # for OpenAI
```

**Verify it worked:**

```bash
cat .env
```

✅ **What success looks like:** You see your key printed, like `ANTHROPIC_API_KEY=sk-ant-abc123...`

### On Windows

```powershell
# Pick ONE of these:
"ANTHROPIC_API_KEY=YOUR_KEY_HERE" | Out-File -FilePath .env -Encoding utf8    # for Claude
"GEMINI_API_KEY=YOUR_KEY_HERE" | Out-File -FilePath .env -Encoding utf8       # for Gemini
"OPENAI_API_KEY=YOUR_KEY_HERE" | Out-File -FilePath .env -Encoding utf8       # for OpenAI
```

**Verify it worked:**

```powershell
Get-Content .env
```

✅ **What success looks like:** You see your key printed.

> **Warning:** The **.env** file contains your secret key. Never share it or commit it to Git.

> **What is a `.env` file?** It's a plain text file that holds configuration values (like secrets) as `KEY=VALUE` pairs, one per line. Docker reads this file and passes the values into the container as environment variables. The leading dot (`.`) makes it a hidden file — it won't show up in Finder or File Explorer by default, but the terminal can see it.

### Minimal working `.env` example

If you just want to get running as fast as possible, your `.env` file only needs **one line** — the API key for whichever provider you chose:

```
ANTHROPIC_API_KEY=sk-ant-api03-your-real-key-here
```

That's it. One line, one key. Everything else is configured by the setup script.

---

## Step 5a: Harden Your API Key File (Required)

These two steps protect your key from accidental exposure. **Run them immediately after creating `.env`.**

> **Security reminder:** These steps are part of the security hardening we mentioned at the top. They're quick but important — don't skip them.

### Restrict file permissions (Mac only)

```bash
# Prevents other users on the same machine from reading your key
chmod 600 .env
```

**Verify it worked:**

```bash
ls -la .env
```

✅ **What success looks like:** `-rw------- 1 yourname staff ... .env` — the key part is `-rw-------` which means only you can read it.

> **Tip:** Windows NTFS file permissions are managed through folder ownership. If you are the sole user on your Windows machine, no additional step is needed. On a shared or corporate Windows machine, right-click `.env` > Properties > Security > ensure only your user account has access.

### Prevent accidental Git commits

If you push any code during the hackathon, this ensures your key is never committed.

```bash
# Mac
echo ".env" >> .gitignore

# Windows
".env" | Out-File -FilePath .gitignore -Append -Encoding utf8
```

**Verify it worked:**

```bash
# Mac
cat .gitignore

# Windows
Get-Content .gitignore
```

✅ **What success looks like:** You see `.env` listed in the output.

> **Warning:** If `.gitignore` does not contain `.env` and you run `git add .`, your key will be staged for commit. Anyone who can see your repo will have access to your billing account.

---

## Step 6: Run OpenClaw with Docker

> **Warning: Docker Desktop MUST be running first.** Open **Docker Desktop** from your Applications (Mac) or Start menu (Windows) and **wait until it fully starts** (whale icon stops animating on Mac, or "Docker Desktop is running" message on Windows). If you skip this, you'll get a `failed to connect to the docker API` error.

You must run these commands from **inside the `openclaw` folder**. If you're not sure, run `pwd` (Mac) or `cd` (Windows) to check.

### On Mac

Type these commands one at a time, pressing **Enter** after each:

```bash
cd ~/openclaw

# Create workspace and config directories
mkdir -p ~/openclaw-workspace ~/.openclaw

# Set environment variables (these tell Docker where to store things)
export OPENCLAW_SANDBOX=1
export OPENCLAW_WORKSPACE_DIR=~/openclaw-workspace
export OPENCLAW_CONFIG_DIR=~/.openclaw

# Build the image and start OpenClaw (this does everything)
./docker-setup.sh
```

### On Windows

```powershell
cd ~\openclaw

# Create workspace and config directories
mkdir "$HOME\openclaw-workspace" -Force
mkdir "$HOME\.openclaw" -Force

# Set environment variables
$env:OPENCLAW_SANDBOX="1"
$env:OPENCLAW_WORKSPACE_DIR="$HOME\openclaw-workspace"
$env:OPENCLAW_CONFIG_DIR="$HOME\.openclaw"

# Build the image and start OpenClaw (this does everything)
bash ./docker-setup.sh
```

> **Tip:** If `bash` is not recognized on Windows, use **Git Bash** (installed with Git in Step 4) instead of PowerShell to run the setup script.

The setup script will:
1. **Build** the Docker image locally (first run takes **5-15 minutes** — you'll see a LOT of text scrolling by, that's normal!)
2. Run the **onboarding wizard** — follow the prompts
3. **Start** the gateway via Docker Compose
4. Generate a **gateway token** and save it to `.env`

✅ **What success looks like:** The scrolling text stops, and you see messages about containers being created and started.

❌ **If you see errors:** Check the Troubleshooting section below.

**Verify containers are running:**

```bash
docker compose ps
```

✅ **What success looks like:** You see a table with containers listed and their status as "running" or "Up".

---

## Step 6a: Harden docker-compose.yml (Required)

Before opening the dashboard, apply these security controls to the Docker Compose configuration. These prevent the container from running with unnecessary privileges on your personal machine.

> **Security reminder:** This is the Docker security hardening pillar we mentioned at the top. It locks down the container so it can only do what it needs to — nothing more.

### Open the file

```bash
# Mac
open -e docker-compose.yml        # opens in TextEdit
# or use any editor: nano docker-compose.yml

# Windows
notepad docker-compose.yml
```

### Find the `openclaw` service block

It will look something like this:

```yaml
services:
  openclaw:
    image: openclaw:local
    ports:
      - "127.0.0.1:18789:18789"
    env_file:
      - .env
```

### Complete hardened service block (copy-paste ready)

**Replace the entire `openclaw` service block** in `docker-compose.yml` with this. Select everything from `services:` down to the last line of the block, delete it, and paste this in:

```yaml
services:
  openclaw:
    image: openclaw:local
    user: "1000:1000"               # run as non-root; prevents privilege escalation
    read_only: true                 # container filesystem is read-only
    cap_drop:
      - ALL                         # drop all Linux kernel capabilities
    security_opt:
      - no-new-privileges:true      # process cannot gain new privileges at runtime
    tmpfs:
      - /tmp                        # allow writes only to /tmp
    deploy:
      resources:
        limits:
          cpus: '2.0'               # prevent runaway inference from freezing your laptop
          memory: 4G
    ports:
      - "127.0.0.1:18789:18789"    # explicit localhost-only binding; no external exposure
    env_file:
      - .env
    network_mode: "bridge"          # default, but explicit — isolates container from host network
```

**What this adds over the basic block:**

- **CPU/Memory limits** — caps at 2 CPU cores and 4 GB RAM so a runaway inference job cannot freeze your laptop
- **`network_mode: bridge` + `127.0.0.1:` binding** — ensures zero external network exposure; the service is unreachable from outside your machine
- **`user`, `read_only`, `cap_drop`, `no-new-privileges`** — prevents container processes from escalating privileges or writing outside `/tmp`

> **Tip:** YAML indentation is strict — use **spaces, not tabs**. Each nested line must be indented with exactly 2 or 4 spaces (match whatever the rest of the file uses).

> **Warning:** If OpenClaw fails to start after this change and shows a `permission denied` error in the logs (`docker compose logs openclaw`), the container image may require running as root. In that case, remove the `user: "1000:1000"` line only and keep the remaining controls. Ask your hackathon organizer if you are unsure.

### Save the file and restart

**Save the file** (Cmd+S on Mac, Ctrl+S on Windows), close the editor, and go back to your terminal:

```bash
docker compose down
docker compose up -d
```

**Verify containers are running:**

```bash
docker compose ps
```

✅ **What success looks like:** Containers show status "running" or "Up".

❌ **If containers show "exited" or you see errors:** See the Troubleshooting section below, especially the YAML syntax error row.

---

## Understanding Ports and Network Binding

OpenClaw exposes **port 18789** by default. Here's what you need to know:

| Topic | Details |
|-------|---------|
| **Default port** | `18789` — this is where the dashboard and gateway listen |
| **Port conflict** | If you see `Port already in use`, another app is on 18789. Fix: change `"127.0.0.1:18789:18789"` to e.g. `"127.0.0.1:18790:18789"` in `docker-compose.yml`, then access via `http://127.0.0.1:18790` |
| **localhost vs 0.0.0.0** | The hardened config binds to `127.0.0.1` (localhost only) — other devices on your network **cannot** access it. If you need LAN access (e.g., testing from a phone), change to `"0.0.0.0:18789:18789"`, but understand this exposes the service to your entire network |
| **HTTPS** | For hackathon use, HTTP on localhost is fine. For production or public-facing setups, put a reverse proxy (nginx, Caddy, or Traefik) in front of OpenClaw to terminate TLS. This is beyond the scope of this guide |
| **Custom domain** | To use a real domain instead of `localhost`, point your DNS to the host machine's IP and use a reverse proxy with an SSL certificate (e.g., Let's Encrypt via Caddy) |

---

## Step 6b: Start the Gateway

The **gateway** is the part of OpenClaw that connects your browser to the AI. Think of it like a receptionist — it receives your requests and routes them to the right place.

> **When do you need this?** The setup script (`./docker-setup.sh`) starts the gateway automatically the first time. But if you restart your computer, close Docker, or stop the containers, you'll need to start the gateway again manually.

### Start the gateway

Make sure you're in the openclaw folder first:

```bash
# Mac
cd ~/openclaw

# Windows
cd ~\openclaw
```

Then start all containers (including the gateway):

```bash
docker compose up -d
```

> **What does `-d` mean?** It stands for "detached" — it runs everything in the background so you can keep using your terminal. Without `-d`, the terminal would be locked up showing logs until you press Ctrl+C.

✅ **What success looks like:** You see messages like:

```
[+] Running 2/2
 ✔ Container openclaw-gateway-1  Started
 ✔ Container openclaw-1          Started
```

**Verify the gateway is running:**

```bash
docker compose ps
```

✅ **What success looks like:** You see a table with containers listed and their status as "running" or "Up".

❌ **If the gateway won't start:** Try stopping everything first, then starting fresh:

```bash
docker compose down
docker compose up -d
```

If it still fails, check the logs for error details:

```bash
docker compose logs openclaw
```

> **Quick reference — all the commands you'll use day-to-day:**
>
> | What you want to do | Command |
> |---|---|
> | Start OpenClaw & gateway | `docker compose up -d` |
> | Stop OpenClaw | `docker compose down` |
> | Restart OpenClaw | `docker compose down && docker compose up -d` |
> | Check if it's running | `docker compose ps` |
> | See error logs | `docker compose logs openclaw` |
> | Get dashboard URL | `docker compose run --rm openclaw-cli dashboard --no-open` |

### Docker Commands Cheat Sheet

If you're new to Docker, here's what these commands actually do:

| Command | What it does | When to use it |
|---------|-------------|----------------|
| `docker compose up -d` | Starts all containers in the background | Starting OpenClaw after a reboot |
| `docker compose down` | Stops and removes containers (data/volumes preserved) | Shutting down OpenClaw |
| `docker compose down -v` | Stops containers AND deletes volumes (resets state) | Full reset / cleanup |
| `docker compose ps` | Shows running containers and their status | Checking if things are running |
| `docker compose logs openclaw` | Shows the OpenClaw container's log output | Debugging when something goes wrong |
| `docker compose logs -f openclaw` | Follows logs in real-time (Ctrl+C to stop) | Watching startup or debugging live |
| `docker compose restart` | Restarts containers without removing them | Quick restart after a config change |

### Updating OpenClaw

To pull the latest code and rebuild:

```bash
cd ~/openclaw          # Mac
cd ~\openclaw          # Windows

git pull origin main
docker compose down
docker compose build --no-cache
docker compose up -d
```

> **Tip:** The `--no-cache` flag forces Docker to rebuild from scratch. This takes longer but ensures you get a clean build with no stale layers.

---

## Step 7: Open OpenClaw in Your Browser

The dashboard URL **includes your token** — you can't just go to `localhost:18789` directly or you'll get a `gateway token missing` error. Use the command below to get the correct URL:

```bash
# This prints the full dashboard URL with your token embedded
docker compose run --rm openclaw-cli dashboard --no-open
```

✅ **What success looks like:**

```
Dashboard URL: http://127.0.0.1:18789/?token=abc123def456ghi789
```

**Copy the full URL** (including the `?token=...` part) and **paste it into your browser** (Chrome, Firefox, Safari, Edge — any will work). The token is saved in your browser automatically — you only need to do this once.

If the command above doesn't work, you can build the URL manually:

```bash
# Mac — get your token
cat ~/.openclaw/openclaw.json | grep token

# Windows — get your token
Get-Content "$HOME\.openclaw\openclaw.json" | Select-String "token"
```

Then open: `http://127.0.0.1:18789/?token=YOUR_TOKEN_HERE`

> **Tip:** If the page doesn't load, wait a minute and refresh — OpenClaw may still be starting.

> **Security note:** Never bookmark or share this URL. The `?token=...` query parameter grants full access to your OpenClaw instance. After your first login the token is saved as a browser cookie, so subsequent visits to `http://127.0.0.1:18789` will work without the token in the URL. Clear your browser history for this address when the hackathon ends (see Cleanup).

---

## Post-Setup Validation Checklist

After completing all the steps, run through this quick checklist to confirm everything is working:

- [ ] **Docker running:** `docker --version` returns a version number
- [ ] **Containers up:** `docker compose ps` shows containers with status "running" or "Up"
- [ ] **No crash loops:** Run `docker compose ps` again after 30 seconds — containers still show "Up" (not "Restarting")
- [ ] **Dashboard loads:** Opening the token URL in your browser shows the OpenClaw dashboard
- [ ] **Chat works:** Send a test message like "Hello, what can you do?" and get a response within 30 seconds
- [ ] **API key secured:** `cat .env` (Mac) or `Get-Content .env` (Windows) shows your key, and `.gitignore` contains `.env`

> **If any check fails**, see the Troubleshooting section below. The most common issues are: containers exited (restart them), dashboard loads but chat doesn't respond (API key issue or container still initializing — wait 1-2 minutes).

---

## Troubleshooting

Don't panic — errors are normal, especially the first time. Find your error message in the table below.

### Common Errors

| Problem | What it means | Fix |
|---------|--------------|-----|
| **`command not found: docker`** or **`docker is not recognized`** | Docker isn't installed, or your terminal was opened before Docker was installed. | Close your terminal, reopen it, and try `docker --version` again. If it still fails, re-do Step 1. |
| **`failed to connect to the docker API`** or **`Cannot connect to Docker daemon`** | Docker Desktop is not running. | Open Docker Desktop from your Applications (Mac) or Start menu (Windows). **Wait 1-2 minutes** until it fully starts, then retry your command. |
| **`No such file or directory`** | You're not in the right folder. | Run `pwd` (Mac) or `cd` (Windows) to see where you are. Then type `cd ~/openclaw` (Mac) or `cd ~\openclaw` (Windows) to get to the right place. |
| **`no configuration file provided: not found`** | You're in the wrong folder — Docker can't find `docker-compose.yml`. | Run `cd ~/openclaw` (Mac) or `cd ~\openclaw` (Windows) first. |
| **`empty section between colons`** or **`OPENCLAW_CONFIG_DIR not set`** | You're missing environment variables. | Re-run the `export` commands (Mac) or `$env:` commands (Windows) from Step 6. You need to do this every time you open a new terminal. |
| **`unable to get image 'openclaw:local'`** | The Docker image hasn't been built yet. | Run `./docker-setup.sh` instead of `docker compose up -d`. See Step 6. |
| **`Port already in use`** | Something else is using the port, or a previous run didn't stop cleanly. | Run `docker compose down`, wait a few seconds, then `docker compose up -d` again. |
| **`Permission denied`** (Mac) | Docker can't access your files. | Open Docker Desktop > Settings > Resources > File Sharing — add your home folder. |
| **`Permission denied`** (Windows) | You need admin rights. | Close PowerShell, right-click it in the Start menu, choose **"Run as administrator"**, and retry. |
| **`git not recognized`** or **`command not found: git`** | Git isn't installed. | Install Git first (see Step 4), then **close and reopen your terminal**. |
| **`API key not found`** | The `.env` file is missing or empty. | Check it exists: `cat .env` (Mac) or `Get-Content .env` (Windows). If empty or missing, redo Step 5. Then restart: `docker compose down && docker compose up -d`. |
| **`unauthorized: gateway token missing`** | You opened `localhost:18789` without the token in the URL. | Run `docker compose run --rm openclaw-cli dashboard --no-open` to get the full URL with token included, then open that URL. See Step 7. |
| **Page won't load in browser** | Containers may have crashed. | Run `docker compose ps`. If containers show "exited", run `docker compose down` then `docker compose up -d`. Wait a minute and try again. |
| **`network timeout`** or **`connection refused`** | Internet issue, or corporate/school WiFi blocking Docker. | Check your internet connection. If on corporate/school WiFi, try a personal mobile hotspot. |
| **Screen shows a wall of text scrolling fast** | That's normal! Docker is building the image. | Just wait. It can take **5-15 minutes** the first time. Don't close the terminal. |
| **Terminal seems frozen / stuck** | It's probably still working on something. | Wait 2-3 minutes. If truly stuck (nothing happening for 5+ minutes), press **Ctrl+C** to cancel and try the command again. |
| **`disk space`** or **`no space left on device`** | Docker images are large and your disk is full. | Free up at least **10 GB** of disk space (delete old files, empty trash) and retry. |
| **`YAML syntax error`** or container won't start after editing docker-compose.yml | You probably used tabs instead of spaces, or the indentation is wrong. | Re-open `docker-compose.yml` and re-copy the **entire** hardened block from Step 6a. Make sure you use **spaces, not tabs**. |
| **Image pull fails** (`manifest unknown`, `pull access denied`) | The Docker image name is wrong, or you need to build locally. | Run `./docker-setup.sh` to build locally. If pulling from a registry, check the image name in `docker-compose.yml`. |
| **Permission denied on volumes** (Linux/Mac) | Docker can't write to mounted directories. | Run `chmod -R 777 ~/openclaw-workspace ~/.openclaw` to fix permissions. On Docker Desktop, also check Settings > Resources > File Sharing. |
| **DNS resolution failed** (`Could not resolve host`) | Your machine can't resolve DNS, often on restricted networks. | Try `ping google.com`. If it fails, switch networks or set DNS to `8.8.8.8` in your network settings. |
| **`TLS handshake timeout`** during build | VPN or firewall is blocking Docker registry traffic. | Disconnect VPN, or try a personal hotspot. See the Prerequisites section for proxy/firewall guidance. |

### OpenClaw-Specific Issues

| Problem | What it means | Fix |
|---------|--------------|-----|
| **URL printed but nothing loads** | The container is still starting up. The URL is printed before the service is fully ready. | Wait 1-2 minutes and refresh the page. Run `docker compose logs -f openclaw` to watch progress — look for "ready" or "listening" messages. |
| **Dashboard loads but chat doesn't respond** | The AI backend isn't connected — usually an API key issue or the provider is rate-limiting you. | Check your `.env` file has the correct key. Run `docker compose logs openclaw` and look for `401`, `403`, or `rate limit` errors. Verify your API key is valid and has credits remaining at the provider's console. |
| **Dashboard is frozen or unresponsive** | The container may be out of memory or the browser tab crashed. | Refresh the page. If still frozen, restart: `docker compose restart`. Check resource usage with `docker stats`. |
| **Chat times out after a long wait** | The AI provider is slow or the request is too large. | Try a shorter prompt. Check the provider's status page (e.g., status.anthropic.com). If persistent, restart the container. |
| **Gateway token generation fails** | The onboarding step that creates the token didn't complete. | Check if the token file exists: `cat ~/.openclaw/openclaw.json` (Mac) or `Get-Content "$HOME\.openclaw\openclaw.json"` (Windows). If missing or empty, run `./docker-setup.sh` again to re-run onboarding. |
| **`openclaw doctor` or health check fails** | Internal services didn't start properly. | If the container supports it, run `docker compose exec openclaw openclaw doctor --fix`. Otherwise, do a full reset: `docker compose down -v && ./docker-setup.sh`. |

### Recovering a Lost Gateway (Containers Stopped or Crashed)

Sometimes Docker containers stop unexpectedly — your laptop went to sleep, Docker Desktop quit, your machine restarted, or the container simply crashed. When this happens, you'll see errors like "connection refused," "page won't load," or the dashboard just goes blank.

**Don't worry — your data and API key are safe.** The containers are just stopped. Here's how to get everything back:

#### Step 1: Open your terminal and navigate to the openclaw folder

```bash
# Mac
cd ~/openclaw

# Windows
cd ~\openclaw
```

#### Step 2: Check what happened

```bash
docker compose ps -a
```

> **What does `-a` mean?** It shows ALL containers, including stopped ones. Without `-a`, you only see running containers (which would show nothing if everything crashed).

You'll likely see something like:

```
NAME                    STATUS
openclaw-1              Exited (137) 2 hours ago
openclaw-gateway-1      Exited (137) 2 hours ago
```

The word **"Exited"** confirms the containers stopped. The number in parentheses is an exit code — don't worry about what it means.

#### Step 3: Re-set your environment variables

Environment variables are lost when you close your terminal or restart your machine. You need to set them again:

```bash
# Mac
export OPENCLAW_SANDBOX=1
export OPENCLAW_WORKSPACE_DIR=~/openclaw-workspace
export OPENCLAW_CONFIG_DIR=~/.openclaw
```

```powershell
# Windows
$env:OPENCLAW_SANDBOX="1"
$env:OPENCLAW_WORKSPACE_DIR="$HOME\openclaw-workspace"
$env:OPENCLAW_CONFIG_DIR="$HOME\.openclaw"
```

#### Step 4: Stop the old containers cleanly, then restart

```bash
docker compose down
docker compose up -d
```

> **Why `down` first?** Even though the containers are already stopped, `docker compose down` removes the old container state cleanly. Starting fresh avoids leftover conflicts.

#### Step 5: Verify everything is running

```bash
docker compose ps
```

✅ **What success looks like:** Containers show status "running" or "Up".

#### Step 6: Get your dashboard URL again

Your gateway token is still saved — you just need to retrieve it:

```bash
docker compose run --rm openclaw-cli dashboard --no-open
```

If that doesn't work, get the token manually:

```bash
# Mac
cat ~/.openclaw/openclaw.json | grep token

# Windows
Get-Content "$HOME\.openclaw\openclaw.json" | Select-String "token"
```

Then open: `http://127.0.0.1:18789/?token=YOUR_TOKEN_HERE`

✅ **You're back!** The gateway is running and you can use OpenClaw again.

#### If it STILL won't start — full reset (last resort)

If the steps above don't work, do a complete teardown and rebuild. **This does NOT delete your API key or workspace files** — it only rebuilds the Docker containers.

```bash
# Stop and remove everything
docker compose down -v

# Re-set environment variables (see Step 3 above)

# Rebuild from scratch
./docker-setup.sh
```

This re-runs the full setup (5-15 minutes) but starts completely fresh. Your `.env` file (API key) and workspace folder are untouched.

> **When would you need this?** After a Docker Desktop update, after a major OS update, or if the containers got corrupted somehow. It's rare, but it fixes almost everything.

---

### What to Do If Nothing Above Helps

Before asking for help, gather this information — it will help the mentor solve your problem much faster:

1. **The exact error message** — screenshot it or copy-paste the text
2. **Which step you're on** (e.g., "I'm on Step 6, running `docker compose up`")
3. **Mac or Windows?** (and which chip / OS version)
4. **Output of `docker compose logs openclaw`** — copy the last 30 lines
5. **What you already tried** (e.g., "I restarted Docker and tried again")

**Where to ask for help:**

| Channel | Best for |
|---------|----------|
| **Hackathon mentor (in person)** | Fastest help — raise your hand |
| **Hackathon Slack/Discord channel** | Remote help, include error details above |
| **OpenClaw GitHub Issues** (https://github.com/openclaw/openclaw/issues) | Bugs in OpenClaw itself |
| **Docker Community Forums** (https://forums.docker.com) | Docker-specific problems |
| **Stack Overflow** (tag: `docker`, `docker-compose`) | General troubleshooting |
| **Ask a neighbor** | They might have hit the same issue 5 minutes ago |

> **Remember:** There are no stupid questions. Everyone was a beginner once. The mentors are here specifically to help you.

---

## After the Hackathon: Cleanup

When the hackathon is over, clean up to **remove your API key and free disk space**. Steps 1-4 and 6 are required; the rest are optional.

### 1. Stop and remove OpenClaw containers and volumes

```bash
cd ~/openclaw          # Mac
cd ~\openclaw          # Windows

docker compose down -v
```

### 2. Remove the Docker image (Required)

The `docker compose down` command stops containers but does **not** remove the built image. Do this explicitly:

```bash
docker rmi openclaw:local
```

**Verify the image is gone:**

```bash
docker images | grep openclaw
```

✅ **What success looks like:** No output (nothing is printed).

> **Tip:** If you want to remove all unused Docker images at once (not just OpenClaw), run `docker image prune -a`. This frees up disk space but removes all images not tied to a running container.

### 3. Securely delete your `.env` file (Required)

Do not just delete the `.env` file — overwrite it first so the key cannot be recovered from disk.

```bash
# Mac / Linux
shred -u ~/openclaw/.env

# Windows (overwrite then delete)
(Get-Content "$HOME\openclaw\.env") -replace '.', '0' | Set-Content "$HOME\openclaw\.env"
Remove-Item "$HOME\openclaw\.env"
```

### 4. Revoke your API key (Required)

Even after deleting the `.env` file, revoke the key from the provider's console to ensure it cannot be used by anyone who may have seen it.

| Provider | Direct revoke URL |
|----------|------------------|
| **Anthropic** | https://console.anthropic.com/settings/keys |
| **Google Gemini** | https://aistudio.google.com/app/apikey |
| **OpenAI** | https://platform.openai.com/api-keys |

### 5. Delete project files (optional)

```bash
# Mac
rm -rf ~/openclaw ~/openclaw-workspace

# Windows
Remove-Item -Recurse -Force ~\openclaw, ~\openclaw-workspace
```

> **Warning:** This deletes your hackathon project files too. Copy **openclaw-workspace** somewhere safe first if you want to keep your work.

### 6. Clear browser data (Required)

The dashboard URL contains your gateway token in the query string. Clear your browser history to prevent the token from persisting after the hackathon.

| Browser | Steps |
|---------|-------|
| **Chrome / Edge** | Settings > Privacy and Security > Clear browsing data > Browsing history — filter by `127.0.0.1:18789` |
| **Firefox** | History > Clear Recent History |
| **Safari** | History > Clear History |

### 7. Uninstall Docker Desktop (optional)

- **Mac:** Drag Docker from Applications to Trash.
- **Windows:** Settings > Apps > Docker Desktop > Uninstall.

---

If you run into issues not covered here, ask a hackathon mentor for help. You've got this!
