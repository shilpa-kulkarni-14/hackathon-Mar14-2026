# OpenClaw Hackathon Setup Guide

## Overview

**OpenClaw** is an open-source coding assistant that runs in your browser using AI. We use **Docker** to run it in a secure sandbox on your laptop. This guide walks you through installing Docker, getting an AI **API key**, and launching OpenClaw.

**What you need:** Mac or Windows 10/11, internet connection, ~20 minutes, a credit/debit card for the API key (typically costs a few dollars).

---

## Step 1: Install Docker Desktop

### On Mac

1. Go to **https://www.docker.com/products/docker-desktop/** and click **"Download for Mac"**.
   - **Apple Silicon** = Mac made in 2021 or later (M1/M2/M3/M4 chip). **Intel** = older Macs.

> **Tip:** Not sure? Click Apple menu > **"About This Mac"** and check the "Chip" field.

2. Open the downloaded **Docker.dmg**, drag Docker to Applications, then launch **Docker** from Applications.
3. Approve any permission prompts and wait for the whale icon in the menu bar to stop animating (~1-2 min).
4. Verify in Terminal:

```bash
docker --version
```

You should see something like `Docker version 27.5.1, build 9f9e405`.

### On Windows

1. Go to **https://www.docker.com/products/docker-desktop/** and click **"Download for Windows"**.
2. Run the installer with default settings. Click **"Close and restart"** when done.
3. After restart, open **Docker Desktop** from the Start menu. Accept the service agreement, skip sign-in.
4. Wait until it shows **"Docker Desktop is running"** (~1-2 min).

> **Warning:** If you see a message about **"WSL 2"**, follow the on-screen instructions to install it, restart, and reopen Docker Desktop.

5. Verify in PowerShell:

```powershell
docker --version
```

---

## Step 2: Get Your API Key

An **API key** is a secret password that lets OpenClaw talk to an AI service. You only need **one** key from **one** provider.

> **Tip:** Quick comparison:
>
> | Provider | Free Credits | Best For |
> |----------|-------------|----------|
> | **Anthropic (Claude)** | $5 for new accounts | Strong coding and reasoning |
> | **Google (Gemini)** | Generous free tier | Free usage, multimodal |
> | **OpenAI (GPT-4o)** | $5 for new accounts | Wide ecosystem, general purpose |

---

### Option A: Anthropic (Claude)

1. Go to **https://console.anthropic.com/** and sign up or log in.
2. Click **"API keys"** in the left sidebar.
3. Click **"Create Key"**, name it **hackathon**, click **"Create Key"**.
4. Your key appears (starts with `sk-ant-`). Click the **copy icon** and **save it immediately**.

> **Warning:** This is the **only time** the full key is shown. Save it now or you'll need to create a new one.

5. **Set up billing:** Left sidebar > **Settings** > **Billing** > **Add Payment Method**. Consider setting a **usage limit** (e.g., $10).

> **Tip:** New accounts often get **$5 in free credits**.

---

### Option B: Google (Gemini)

1. Go to **https://aistudio.google.com/** and sign in with your Google account.
2. Click **"Get API key"** in the left sidebar.
3. Click **"Create API key"**. If asked to select a project, click **"Create API key in new project"**.
4. Your key appears (starts with `AIzaSy`). Click the **copy icon** and **save it immediately**.

> **Tip:** Gemini has a generous free tier — you likely won't be charged at all. Details at **https://ai.google.dev/pricing**

**Optional billing** (only if you exceed the free tier): Go to **https://console.cloud.google.com/billing** and link a billing account.

---

### Option C: OpenAI (GPT-4o)

1. Go to **https://platform.openai.com/** and sign up or log in.
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

---

## Step 3: Open Your Terminal or CLI

A **terminal** is where you type commands. You'll just copy-paste from this guide.

- **Mac:** Press **Command + Space**, type **Terminal**, press Enter.
- **Windows:** Press the **Windows key**, type **PowerShell**, click **"Windows PowerShell"**.

---

## Step 4: Clone OpenClaw

First, check if **Git** is installed:

```bash
git --version
```

If you see a version number, skip ahead to "Clone the Project." If not:
- **Mac:** Run `xcode-select --install` and follow the prompts.
- **Windows:** Download and install from **https://git-scm.com/download/win** (use all default settings). **Reopen PowerShell** after installing.

### Clone the Project

```bash
# Download OpenClaw
git clone https://github.com/openclaw/openclaw.git

# Enter the project folder
cd openclaw
```

> **Tip:** If the URL doesn't work, ask your hackathon organizer for the correct one.

> **Warning:** If you see `Authentication failed` or `Invalid username or token`, follow the steps below.

### If cloning fails: Authenticate with GitHub

The repo may be private. You need a GitHub account and to authenticate your terminal.

**A. Create a GitHub account (skip if you already have one):**

1. Go to **https://github.com/signup**
2. Enter your email, create a password, and choose a username.
3. Complete the verification and click **"Create account"**.
4. Check your email and verify your account.
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
6. Your browser will open. Paste the code, click **"Authorize"**, and confirm.
7. Back in your terminal, you should see **"Logged in as yourusername"**.

**D. Try cloning again:**

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
```

> **Tip:** If it still fails, ask your hackathon organizer — they may need to add you to the repo, or provide a direct ZIP download.

---

## Step 5: Set Up Your API Key

You need to create a **.env** file **inside the `openclaw` folder** you cloned in Step 4. Make sure your terminal is still in that folder (you should see `openclaw` in your terminal prompt). If not, run `cd openclaw` first.

Run **only one** of these commands, matching your provider:

### On Mac

```bash
# Pick ONE of these — replace YOUR_KEY_HERE with your actual key
echo "ANTHROPIC_API_KEY=YOUR_KEY_HERE" > .env    # for Claude
echo "GEMINI_API_KEY=YOUR_KEY_HERE" > .env       # for Gemini
echo "OPENAI_API_KEY=YOUR_KEY_HERE" > .env       # for OpenAI
```

Verify: `cat .env` — you should see your key printed.

### On Windows

```powershell
# Pick ONE of these — replace YOUR_KEY_HERE with your actual key
"ANTHROPIC_API_KEY=YOUR_KEY_HERE" | Out-File -FilePath .env -Encoding utf8    # for Claude
"GEMINI_API_KEY=YOUR_KEY_HERE" | Out-File -FilePath .env -Encoding utf8       # for Gemini
"OPENAI_API_KEY=YOUR_KEY_HERE" | Out-File -FilePath .env -Encoding utf8       # for OpenAI
```

Verify: `Get-Content .env` — you should see your key printed.

> **Warning:** The **.env** file contains your secret key. Never share it or commit it to Git.

---

## Step 5a: Harden Your API Key File (Required)

These two steps protect your key from accidental exposure. Run them immediately after creating `.env`.

### Restrict file permissions (Mac only)

```bash
# Prevents other users on the same machine from reading your key
chmod 600 .env
```

Verify the permissions were set correctly:

```bash
ls -la .env
# Expected output: -rw------- 1 yourname staff ... .env
```

> **Tip:** Windows NTFS file permissions are managed through folder ownership. If you are the sole user on your Windows machine, no additional step is needed. On a shared or corporate Windows machine, right-click `.env` > Properties > Security > ensure only your user account has access.

### Prevent accidental Git commits

If you push any code during the hackathon, this ensures your key is never committed.

```bash
# Mac
echo ".env" >> .gitignore

# Windows
".env" | Out-File -FilePath .gitignore -Append -Encoding utf8
```

Verify:

```bash
# Mac
cat .gitignore

# Windows
Get-Content .gitignore
```

You should see `.env` listed.

> **Warning:** If `.gitignore` does not contain `.env` and you run `git add .`, your key will be staged for commit. Anyone who can see your repo will have access to your billing account.

---

## Step 6: Run OpenClaw with Docker

> **Warning: Docker Desktop MUST be running first.** Open **Docker Desktop** from your Applications (Mac) or Start menu (Windows) and **wait until it fully starts** (whale icon stops animating on Mac, or "Docker Desktop is running" message on Windows). If you skip this, you'll get a `failed to connect to the docker API` error.

You must run these commands from **inside the `openclaw` folder**.

### On Mac

```bash
cd ~/openclaw

# Create workspace and config directories
mkdir -p ~/openclaw-workspace ~/.openclaw

# Set environment variables
export OPENCLAW_SANDBOX=1
export OPENCLAW_WORKSPACE_DIR=~/openclaw-workspace
export OPENCLAW_CONFIG_DIR=~/.openclaw

# Build the image and start OpenClaw (handles everything)
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

# Build the image and start OpenClaw (handles everything)
bash ./docker-setup.sh
```

> **Tip:** If `bash` is not recognized on Windows, use **Git Bash** (installed with Git) instead of PowerShell to run the setup script.

The setup script will:
1. **Build** the Docker image locally (first run takes **5-15 minutes**)
2. Run the **onboarding wizard** — follow the prompts
3. **Start** the gateway via Docker Compose
4. Generate a **gateway token** and save it to `.env`

When complete, you should see containers running. Verify with:

```bash
docker compose ps
```

---

## Step 6a: Harden docker-compose.yml (Required)

Before opening the dashboard, apply these security controls to the Docker Compose configuration. These prevent the container from running with unnecessary privileges on your personal machine.

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

### Add the hardening block

Under the `openclaw` service, add the following lines at the same indentation level as `image`, `ports`, etc.:

```yaml
    # Security hardening — add these lines
    user: "1000:1000"               # run as non-root user; prevents privilege escalation
    read_only: true                 # container filesystem is read-only
    cap_drop:
      - ALL                         # drop all Linux kernel capabilities
    security_opt:
      - no-new-privileges:true      # process cannot gain new privileges at runtime
    tmpfs:
      - /tmp                        # allow writes only to /tmp (required for runtime temp files)
```

### Complete hardened service block (copy-paste ready)

Replace the entire `openclaw` service block in `docker-compose.yml` with this:

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

### Save and restart

```bash
docker compose down
docker compose up -d
```

Verify containers are running:

```bash
docker compose ps
```

---

## Step 7: Open OpenClaw in Your Browser

The dashboard URL **includes your token** — you can't just go to `localhost:18789` directly or you'll get a `gateway token missing` error. Use the command below to get the correct URL:

```bash
# This prints the full dashboard URL with your token embedded
docker compose run --rm openclaw-cli dashboard --no-open
```

You should see output like:

```
Dashboard URL: http://127.0.0.1:18789/?token=abc123def456ghi789
```

**Copy the full URL** (including the `?token=...` part) and paste it into your browser. The token is saved in your browser automatically — you only need to do this once.

If the command above doesn't work, you can build the URL manually:

```bash
# Mac — get your token
cat ~/.openclaw/openclaw.json | grep token

# Windows — get your token
Get-Content "$HOME\.openclaw\openclaw.json" | Select-String "token"
```

Then open: `http://127.0.0.1:18789/?token=YOUR_TOKEN_HERE`

> **Tip:** If the page doesn't load, wait a minute and refresh — OpenClaw may still be starting.

> **Security note:** Never bookmark or share this URL. The `?token=...` query parameter grants full access to your OpenClaw instance. After your first login the token is saved as a browser cookie, so subsequent visits to `http://127.0.0.1:18789` will work without the token in the URL. Clear your browser history for this address when the hackathon ends (see Cleanup, Step 6).

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| **"no configuration file provided: not found"** | You're in the wrong folder. Run `cd ~/openclaw` (Mac) or `cd ~\openclaw` (Windows) first. |
| **"empty section between colons"** or **OPENCLAW_CONFIG_DIR not set** | You're missing environment variables. Make sure you set both `OPENCLAW_WORKSPACE_DIR` and `OPENCLAW_CONFIG_DIR` when running `docker compose up`. See Step 6. |
| **"unable to get image 'openclaw:local'"** | The image hasn't been built yet. Run `./docker-setup.sh` instead of `docker compose up -d`. See Step 6. |
| **"failed to connect to the docker API"** or **"Cannot connect to Docker daemon"** | Docker Desktop is not running. Open it, **wait until it fully starts** (1-2 min), then retry. |
| **"Port already in use"** | Run `docker compose down`, then `docker compose up -d` again. |
| **"Permission denied" (Mac)** | Docker Desktop > Settings > Resources > File Sharing — add your home folder. |
| **"Permission denied" (Windows)** | Close PowerShell, reopen it with **Run as administrator**. |
| **"git not recognized"** | Install Git first (see Step 4), then reopen your terminal. |
| **"API key not found"** | Check `.env` exists in the openclaw folder (`cat .env` or `Get-Content .env`). Restart with `docker compose down && docker compose up -d`. |
| **"unauthorized: gateway token missing"** | You opened `localhost:18789` without the token. Run `docker compose run --rm openclaw-cli dashboard --no-open` to get the full URL with token included, then open that URL instead. See Step 7. |
| **Page won't load** | Run `docker compose ps`. If containers show "exited", run `docker compose down` then `docker compose up -d`. |

---

## After the Hackathon: Cleanup

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

Verify the image is gone:

```bash
docker images | grep openclaw
# Expected: no output
```

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

### 6. Revoke API key + clear browser data (Required)

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

If you run into issues not covered here, ask a hackathon mentor for help.
