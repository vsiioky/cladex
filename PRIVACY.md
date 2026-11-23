# Cladex privacy policy

Last updated: 2026-11-24
Contact: the Issues of this repository (https://github.com/vsiioky/cladex/issues)
This page is hosted at: https://github.com/vsiioky/cladex/blob/main/PRIVACY.md

## In short

- Cladex is a remote control for AI coding agents that run on your own computers. It has two parts: an app for the G2 glasses (installed from Even Hub) and a program with one system service that you install on each of your computers.
- The app sends data only to your own computers. There is no Cladex server and no Cladex account. The developer receives no data from the app or from the program.
- There is no analytics, no advertising and no tracking, in the app or in the program.
- Cladex is an independent project. It is not affiliated with or endorsed by Anthropic, OpenAI, Even Realities or the makers of Hermes and OpenClaw. Product names belong to their owners.

## What data the app handles

- Session content: the text of your sessions with Claude Code, Codex, Hermes and OpenClaw (your messages, the answers, tool requests that may contain commands and file paths, questions the agent asks you), session titles, folder names and the names of your computers.
- Your voice, only while you dictate (see "Voice").
- Pairing data: the address of each of your computers that you typed or that a computer you approved named, and the access token that computer gave to this phone.
- Settings: interface language, favourites, queued messages and similar state of the app.

## Where the data goes

- From the phone, requests go only to the Cladex program on computers you set up yourself. They use HTTPS to each computer's own address on Tailscale (a name ending in .ts.net). The phone sends its access token only to addresses built into the app, to addresses that you typed and that a computer has confirmed, and to addresses named by a computer that approved the phone.
- The phone may talk to any one of your computers, and that computer passes requests on to your other computers. Nothing passes through a server of the developer.
- Tailscale Funnel: to let a phone that is not on your tailnet reach a computer, the computer's program is published with Tailscale Funnel. Traffic then crosses Tailscale's network, and the computer's .ts.net address can be resolved from the internet. Requests are accepted only with the token of a phone you approved; the pairing code is shown only on your computer and expires. Tailscale's own terms and privacy policy apply to this part.
- Session content stays between your phone, your computers and the AI agents you run on them. The agents themselves (Claude Code, Codex, Hermes, OpenClaw) talk to their own providers under the providers' terms. Cladex does not take part in that and has no access to it beyond what your computer shows the app.

## Voice

When you hold the touchpad of the glasses to dictate, the glasses microphone records a clip. The app sends the clip to your own computer. The computer turns it into text with the speech service you set up there, ElevenLabs or OpenAI, using your own API key stored on that computer. That provider receives the audio and handles it under its own terms. No key is stored in the app or sent to the developer. The developer never receives the clip.

## Optional push notifications

Push is off until you set it up on a computer. When on, the computer sends short messages (the computer's name, the agent, and what happened, for example a session waiting for you) to the public ntfy service, ntfy.sh, which delivers them to your own notification app. Session titles are included only if you leave that option on. The topic name you choose is the only secret protecting those messages: anyone who knows it can read them. Use a long random topic. The developer does not receive push messages.

## What is kept on the phone

The app keeps its settings, the list of computers and their addresses, the access tokens of your phone, favourites, queued messages and the state of the screens, in the storage that Even Hub gives the app. This data stays on the phone. Removing a computer or an address in the app's settings makes the app forget it. Uninstalling the app or clearing its data removes everything. Demo mode uses made-up data and sends nothing.

## What is kept on your computers

The Cladex program keeps its configuration, the list of approved phones (with the check data of their tokens, not the tokens in the clear), and local log files in a folder in your home directory. Your session history stays where the AI agents keep it. You can read, move or delete all of it.

## Installing, links and the support page

- The install line downloads Cladex from GitHub (github.com/vsiioky/cladex) and, on Linux and Windows, Node.js from nodejs.org. Those sites see the request as they see any download. After that the program contacts neither of them by itself: it does not check for updates on its own.
- Buttons and links that lead to a web page (the download page of Tailscale or of an AI agent, the Issues of this repository, the support page ko-fi.com/cladex) open that page in your browser only when you press them. Nothing is sent to those sites otherwise.
- Supporting the project is voluntary and happens on Ko-fi under its own terms. The app for the glasses carries no request for support.

## What Cladex does not do

- It has no developer server and no account.
- It does not collect analytics or crash reports and does not send them anywhere.
- It does not sell or share data, and it shows no advertising.
- It does not bundle any API key or secret in the app.

## Permissions

- network: lets the app reach the Cladex program on your computers (addresses ending in .ts.net).
- g2-microphone: lets the app record your voice, only while you hold the touchpad to dictate.

## Revoking a phone and deleting data

- On any computer you set up, run `cladex device revoke <phone name>`, or use the list of phones in the Cladex app for Mac. The phone's token stops working at once on that computer, and the other computers learn it from the shared list.
- On the phone, remove a computer in the app's settings, or uninstall the app.
- To stop push, turn it off on the computer.
- To remove Cladex from a computer, run `cladex uninstall`: it removes the service, the hooks in the settings of Claude, the keys, the addresses in Tailscale and the data folder.

## Children, changes, contact

Cladex is a developer tool and is not directed at children. If this policy changes in a way that matters, the new version is published at the address above with a new date. Questions: the Issues of this repository (https://github.com/vsiioky/cladex/issues). The source of Cladex is not published; this repository holds only builds and instructions.
