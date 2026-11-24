# Cladex

**English** | [Русский](README.ru.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Español](README.es.md) | [Italiano](README.it.md) | [简体中文](README.zh-Hans.md) | [繁體中文](README.zh-Hant.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cladex)

Cladex is a remote control for the AI agents that work on your own computers, shown on the Even G2 glasses.

- You install a program on each computer where your AI agents work. It is a Mac app with its own window.
- The glasses (through the Even app on your phone) show your agents, their sessions and their questions, and let you answer by touch or by voice.
- Everything goes from your phone to your own computers by their own addresses. There is no Cladex server and no Cladex account.
- Works with Claude Code, Codex, Hermes and OpenClaw.
- This repository holds only the builds and the instructions. The source is not published.

## Install with your AI agent

If you work with an AI agent that has a shell on this computer (Claude Code, Codex, Hermes, OpenClaw or another), you can let it do the install. Copy this text into the agent:

```
Install Cladex on this computer. Read https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md and follow it step by step. Stop and ask me where it says so.
```

The agent downloads Cladex from this repository, sets it up and connects your agents and your phone by itself. It stops and asks you where only you can go on: signing in to Tailscale, opening the computer's address to the internet (it asks before it does), Hermes and OpenClaw (they need your yes), a speech key (you type it at a hidden prompt, never into the chat), the Claude dispatcher in the Claude app, and the code on your phone. It never uses administrator rights.

Read [AGENT-INSTALL.md](AGENT-INSTALL.md) first: it is short, and it is exactly what the agent will follow. An agent without internet access can be given the file itself instead of the address.

## What you need

- A Mac with an Apple chip (M1 or newer) and macOS 15 or newer. Linux and Windows are a preview without a window (see Install); a Mac with an Intel chip has no build yet.
- A free Tailscale account for personal use (tailscale.com/download/mac). It gives the computer an address on the internet. You do not install Tailscale on the phone.
- At least one AI agent on the computer, signed in: Claude Code (claude.com/download), Codex (developers.openai.com/codex/app), Hermes (hermes-agent.nousresearch.com/docs/getting-started/installation) or OpenClaw (docs.openclaw.ai/install). Claude Code needs a paid claude.ai plan.
- The Even G2 glasses and the Even app on your phone.

## Install

Pick your computer. Each one has its own command and its own way to run it.

### Mac with an Apple chip (M1 or newer)

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

How to run it:

1. Press Cmd+Space, type Terminal and press Enter. A window with a text line opens.
2. Copy the command above, paste it into that window (Cmd+V) and press Enter.
3. Wait until it says what it did. The script never asks for your password.

What you see next: the Cladex window opens and leads you through the first setup, one step at a time (the section below).

What the script does: downloads the disk image, checks its checksum, its signature and its notarization by Apple, copies Cladex.app into Applications, closes the image and opens Cladex. It changes nothing until the checks pass. If /Applications is not writable it uses the Applications folder in your home folder and says so. If Cladex is running, it asks you to quit it first. Options: `--no-open`, `--dir <folder>`, `--help` (after the line: `| sh -s -- --no-open`).

The manual way: open https://github.com/vsiioky/cladex/releases, download cladex-arm64.dmg, open it, drag Cladex to Applications and open it from there. The same page has SHA256SUMS to compare the checksum (`shasum -a 256 cladex-arm64.dmg`).

Status: verified on a real Mac with the signed and notarized disk image of the release.

### Mac with an Intel chip

There is no build yet. The same command says so in one sentence and stops without changing anything. Look at the releases page for news.

### Linux (x64 and arm64), preview

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

How to run it:

1. Open a terminal (on most desktops: Ctrl+Alt+T, or find "Terminal" in the menu of programs).
2. Copy the command above, paste it (Ctrl+Shift+V) and press Enter.
3. Answer the questions that appear in the same window. Nothing changes until you answer.

What you see next: no window. The script puts Cladex under ~/.g2-claude, puts the command `cladex` on your path and starts `cladex setup`, which asks its questions in the terminal. When it ends, run these commands one after another: `cladex gateway init`, then `cladex gateway publish`, then `cladex pair` (it prints the address of the computer and a code). Add `--no-setup` after `| sh -s --` to only install. It needs curl, tar, gzip and xz (the package xz-utils), never uses sudo, and downloads Node.js 22 itself and checks its checksum.

Status: preview. Tested in a Debian container (arm64): the install, `cladex --version` and `cladex setup --print`. Not tested on a real Linux computer, with real services (systemd), Tailscale or agents.

### Windows 10 and 11, preview

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

How to run it:

1. Open the Start menu, type PowerShell and press Enter (an ordinary window, not "as administrator").
2. Copy the command above, paste it (right mouse click pastes) and press Enter.
3. Answer the questions that appear in the same window. Nothing changes until you answer.

What you see next: no window of Cladex. The script puts Cladex under your user folder (.g2-claude), adds its command folder to the path of your user and starts `cladex setup`, which asks its questions in PowerShell. When it ends, run: `cladex gateway init`, then `cladex gateway publish`, then `cladex pair`. To only install, set `$env:CLADEX_NO_SETUP = '1'` before the line. No administrator rights are used.

Status: preview. The script was only read and checked by hand and by static tests: it has not been run on a real Windows computer yet, and PowerShell did not parse it on the machine where it was written.

## The first setup

On a Mac, Cladex names each next step in its window; on Linux and Windows `cladex setup` and `cladex status` name them in the terminal. In short:

1. Open Cladex. Read the install plan and answer its one question. Nothing changes until you answer.
2. Install Tailscale (tailscale.com/download/mac), open it and sign in. Rename the computer if its name holds your own name.
3. In the Tailscale pages, in a browser: turn on MagicDNS and "Enable HTTPS" (console.tailscale.com/admin/dns) and add Funnel to the policy (console.tailscale.com/admin/acls).
4. In Cladex click "Publish address" and write down the address of the computer. It looks like name.tailnet.ts.net and can take up to 10 minutes to appear on the internet.
5. Install and sign in to an AI agent from the list above. Cladex does not install other programs, and finds the agent by itself after "Check again". For Claude Code the window also shows a one-time dispatcher step.
6. Voice is optional and needs your own key from ElevenLabs (elevenlabs.io/app/settings/api-keys) or OpenAI (platform.openai.com/api-keys). Paste it in Cladex, Settings.

## The app for the glasses

The Cladex app for the glasses is in the Even beta channel. It is there by invitation until Even lists it in its catalog, and the invitation is sent to the email of your Even account. To ask for one, open an issue in this repository (https://github.com/vsiioky/cladex/issues) with the title "Beta invitation". Do not write your email in the issue: an issue is public, and the answer will say how to send the email privately. After the invitation, install the beta build in the Even app on your phone.

## Connect the phone

1. In Cladex on the computer click "Connect a phone": the address of the computer and a code of 8 digits appear.
2. In the Cladex app in the Even app on the phone enter the address and the code, then the 3 digits shown on the computer.
3. Put on the glasses. If they say "No computers", tap the glasses screen: the list is checked again.

## Update

Run the install line of your computer again: on a Mac a running Cladex must be quit first, and the older copy is replaced. On Linux and Windows `cladex update` does the same by itself: it downloads the latest release, checks its checksum, puts it next to the running copy and restarts the service, and if the new version does not answer, the service goes back to the previous one. Your settings and your phones stay.

Once a day Cladex asks GitHub whether there is a newer release (GitHub sees your address on the internet and the version of Cladex, nothing else), and `cladex status` tells you when there is. `cladex update check off` turns this check off and `cladex update check on` turns it on again. While the check is off, fixes of security problems and bugs do not arrive, nothing tells you about a new version, and the app on the glasses, which updates itself through Even, may stop understanding an old version on the computer. Cladex installs a new version by itself only after you allow it with `cladex update auto on`; `cladex update auto off` forbids it again. `cladex update status` shows all of it.

## Remove

In Cladex open Settings, the "Removal" group, "Remove Cladex from this computer...". Or in the Terminal run `cladex uninstall`: it removes everything Cladex installed (the service, the hooks, the settings, the keys, the logs). Then move Cladex.app to the Trash. Tailscale and your AI agents stay.

## Privacy

- There is no Cladex server and no account. The developer receives no data from the app or the program.
- No analytics, no advertising, no tracking.
- Your voice goes only to your own computer and from it to the speech service with your own key.

Full text: [PRIVACY.md](PRIVACY.md). Terms of use: [TERMS.md](TERMS.md).

## About

The source of Cladex is not published. Cladex is independent and is not affiliated with or endorsed by Anthropic, OpenAI, Nous Research, OpenClaw, Even Realities or Tailscale. Product names belong to their owners. Questions and problems: the Issues of this repository.

## Support Cladex

Cladex is free and will stay free. If it helps you, you can support its development: ko-fi.com/cladex.
