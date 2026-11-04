<div align="center">

<img width="100%" alt="header" src="https://capsule-render.vercel.app/api?type=waving&height=210&text=Orex%20Bot&fontAlign=50&fontAlignY=36&fontSize=56&desc=Auto%20Mining%20%7C%20Auto%20Anti-Bot%20Answer%20%7C%20Browser%20Login%20%7C%20Live%20Dashboard&descAlign=50&descAlignY=58"/>

<img alt="typing" src="https://readme-typing-svg.demolab.com?font=Inter&size=18&duration=3000&pause=650&center=true&vCenter=true&width=900&lines=Auto+Mine+OREX+%7C+SHA-256+Proof+of+Work+on+CPU;Auto+Anti-Bot+Answer+%7C+Solved+Locally+and+Silently;Browser+Login+%7C+Or+Paste+an+API+Key;Live+Dashboard+%7C+Hashrate+%7C+Round+%7C+Payout+%7C+Balance;Unattended+Mode+%7C+Run+Inside+Screen"/>

<p>
  <img alt="nodejs" src="https://img.shields.io/badge/Node.js-18+-339933?logo=nodedotjs&logoColor=white"/>
  <img alt="platform" src="https://img.shields.io/badge/Platform-OREX%20Miner-111111"/>
  <img alt="cpu" src="https://img.shields.io/badge/Mining-CPU%20Threads-111111"/>
  <img alt="termux" src="https://img.shields.io/badge/Termux-Supported-111111"/>
  <img alt="author" src="https://img.shields.io/badge/by-Yuurisandesu-111111"/>
</p>

<p>
  <b>Orex Bot</b> is an automated terminal miner for OREX.<br/>
  It is the OREX CLI with automatic anti-bot answers built in. It logs in with your browser or an API key, mines with all of your CPU threads, answers the server verification question locally the moment it appears without printing anything or pausing the screen, and shows a live dashboard with hashrate, round progress, payouts, and balance, all from one command.<br/>
  Built and distributed by <b>Yuurisandesu</b>.
</p>

</div>

---

## Table of Contents

- [Requirements](#requirements)
- [Installation](#installation)
- [Login](#login)
- [Running the Bot](#running-the-bot)
- [Unattended Mode](#unattended-mode)
- [Features](#features)
- [Repository Structure](#repository-structure)
- [Disclaimer](#disclaimer)

---

## Requirements

- Node.js `18` or newer (npm is included with Node.js)
- An OREX account and API key from https://orex.run/dashboard
- `screen` (optional, only for unattended mode)

---

## Installation

This repository only holds the documentation. The program itself is distributed as a package file on the releases page, so there is nothing to clone or build.

### Install Node.js

**Windows:**

1. Go to https://nodejs.org and download the LTS installer
2. Run the installer and follow the setup wizard
3. Open Command Prompt and verify the installation:

```cmd
node -v
npm -v
```

**Linux (Ubuntu / Debian):**

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
node -v
npm -v
```

**macOS:**

```bash
brew install node
node -v
npm -v
```

> If you do not have Homebrew, install it first from https://brew.sh

**Termux (Android):**

```bash
pkg update && pkg upgrade -y
pkg install nodejs curl -y
node -v
npm -v
```

---

### Download the Package

Go to https://github.com/Yuurisan-N1/Orex-Bot/releases/latest and download the file `orex-auto-captcha.tgz`.

**Or download it from the terminal:**

Linux, macOS, and Termux:

```bash
curl -L -o orex-auto-captcha.tgz https://github.com/Yuurisan-N1/Orex-Bot/releases/latest/download/orex-auto-captcha.tgz
```

Windows (PowerShell):

```powershell
Invoke-WebRequest -Uri https://github.com/Yuurisan-N1/Orex-Bot/releases/latest/download/orex-auto-captcha.tgz -OutFile orex-auto-captcha.tgz
```

---

### Install the Package

Open a terminal in the folder where you saved `orex-auto-captcha.tgz` and run:

```bash
npm install -g ./orex-auto-captcha.tgz
```

**If you get a permission error on Linux or macOS**, install it into your home folder instead:

```bash
npm install -g ./orex-auto-captcha.tgz --prefix ~/.local
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

On macOS with zsh, use `~/.zshrc` instead of `~/.bashrc`.

**Verify the installation:**

```bash
orex --version
```

**Verify the anti-bot patch is present (Linux, macOS, Termux):**

```bash
grep -c computeAnswer "$(npm root -g)/@orexdotrun/orex/src/miner.js"
```

The result `2` means the patched version is installed. The result `0` means the original version is installed.

---

## Login

Get your API key at https://orex.run/dashboard. Keys look like `orex_` followed by 48 hex characters.

**Login with an API key:**

```bash
orex login <API_KEY>
```

**Or run the login command without a key and choose a method from the menu:**

```bash
orex login
```

Pick **Log in with your browser** to approve the terminal in your browser, or pick **Paste an API key**. When you are connected over SSH or using Termux there is no local browser, so use the API key method.

The key is stored in `~/.orex/config.json` and is readable only by your user. The login refuses any server address that is not `https://`, so your key is never sent unencrypted.

---

## Running the Bot

**Start mining with the default thread count:**

```bash
orex mine
```

**Choose how many CPU threads to use:**

```bash
orex mine -t 4
```

The default is all cores minus one. The value must be between 1 and the number of cores on your machine.

**All commands:**

| Command | Description |
|---|---|
| `orex` | Open the interactive full-screen menu |
| `orex login [API_KEY]` | Log in through your browser or with an API key |
| `orex mine [-t N]` | Start mining |
| `orex status` | Show balance, total earned, shares, and 10 minute hashrate |
| `orex logout` | Remove the API key from this computer |
| `orex help` | Show the help screen |
| `orex -v` | Show the version |

`orex balance` and `orex whoami` work as aliases of `orex status`.

Press `Ctrl+C` at any time to stop mining cleanly and see the session summary.

---

## Unattended Mode

Run the miner inside `screen` so it keeps going after you close the terminal. This works on Linux, macOS, and Termux.

**Install screen:**

```bash
# Linux (Ubuntu / Debian)
sudo apt-get install -y screen

# macOS
brew install screen

# Termux
pkg install screen -y
```

**Start mining in a detached session:**

```bash
screen -dmS orexn orex mine
```

**Open the session to watch the dashboard:**

```bash
screen -r orexn
```

Press `Ctrl+A` then `D` to detach again without stopping the miner.

On Windows, keep the terminal window open while mining.

---

## Features

### Auto Mining
The miner solves SHA-256 proof of work jobs across all selected CPU threads, with every thread checking a different set of nonces. When a thread finds a hash that meets the job difficulty, the share is submitted right away and the next job is fetched. Jobs that take too long are swapped for a fresh one so the server can lower the difficulty.

### Auto Anti-Bot Answer
When the server answers with a verification question, the bot works out the answer locally and sends it back by itself. Nothing is printed, the screen does not pause, and no file is written, so the output looks exactly the same as the original client. If an answer is not accepted, the bot waits and retries several times before stopping with a message.

### Browser Login
The login opens your browser to approve the terminal with a short login code, and the API key comes back to the terminal automatically. When no browser is available, such as over SSH, the code and link are shown so you can approve from another device, or you can paste an API key instead.

### Live Dashboard
In a terminal the miner runs a full-screen dashboard showing username, uptime, hashrate with a live graph, job progress toward the target difficulty, round countdown with the number of miners, your estimated share of the round, the last payout, your balance, and what you earned this session. The layout adapts to the terminal width, from a full view with the animated gem down to a single status line for narrow screens.

### Round Payout Tracking
Mining pays per round. Each round the network releases a fixed amount of OREX that is split between the miners of that round. The dashboard follows the round in progress, flashes when a payout lands, and keeps a running total of what the session has earned.

### Plain Output Mode
When the output is not a terminal, such as when it is redirected to a log file, the miner prints plain timestamped lines instead of the dashboard. A status line with hashrate, shares, and balance is written every minute, and a line is written for each payout.

### Session Summary
On exit the bot prints the session duration, accepted and rejected shares, total hashes with the average hashrate, OREX earned, and the final balance. Shares that are still inside the current round are noted as they are still paid when the round ends.

### Account Status
`orex status` shows your username, balance, total earned with the share count, the 10 minute average hashrate, and the server in use.

### Secure Config
The API key file is created readable only by your user, server messages are cleaned of control characters before they reach the screen, and logins over an insecure connection are refused except for a local server.

---

## Repository Structure

**Repository:**

```Structure
Orex-Bot/
├── HOWTO.txt       # Quick start guide
├── LICENSE         # License file
└── README.md       # This file
```

---

## Disclaimer

This tool is built for educational and technical exploration purposes. Use it wisely and at your own responsibility.

---

<div align="center">
<img width="100%" alt="footer" src="https://capsule-render.vercel.app/api?type=waving&height=120&section=footer"/>
</div>