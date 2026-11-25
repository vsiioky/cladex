# Changelog

What changed in each version of Cladex, newest first. [Russian](CHANGELOG.ru.md)

## 0.1.7 - 2026-11-25

- What is new is shown in English in every language of the program, without markup.
- The Codex card can refresh the model list from Codex's saved catalog, keeping custom models and a backup, without restarting running sessions.
- Full access from the phone can be allowed or blocked in the Codex card. Allowing it asks for the owner's confirmation.
- Turning on the ChatGPT connection in Settings restores its login item if macOS disabled it. After restarting ChatGPT, you can continue the same local Codex chat on the Mac and the glasses.

## 0.1.6 - 2026-11-24

- OpenClaw models appear by themselves after OpenClaw restarts.
- An old shared Codex service is named as such and can be updated with one button (`cladex product update codex`).
- When something is wrong, the window shows a page that describes the problem instead of the first setup.
- Commands in the window are buttons, and commands in Help are copied with one click.

## 0.1.5 - 2026-11-24

- The list of sessions on the phone and the glasses names each session by its title, its last answer or your first request.
- Sessions of one folder no longer all read as the folder name.
- A session started from the app is named by the first words of your task.
- Codex, Hermes and OpenClaw sessions without a name are no longer named by an id or by a word such as main.

## 0.1.4 - 2026-11-24

- The program shows what is new: before an update in Settings, Updates, and once after it on the main screen.
- `cladex update check` and `cladex update` print what is new.
- `cladex update` accepts `--yes`, like the other commands.

## 0.1.3 - 2026-11-24

- The same as 0.1.2 under a new number, made to check that updating works.

## 0.1.2 - 2026-11-24

- Updates: Cladex looks for a new version once a day and tells you when there is one.
- Update with one button in the window or with `cladex update`.
- Cladex installs a new version by itself only after you allow it.
- The daily check can be turned off.
- A Claude account that has used up its limit is now reported as a limit, not as a failure.
- The window no longer loses the service after many hours.
- Codex is found inside the ChatGPT app.
- A product that is not installed is no longer reported as found.
- A Support link in the sidebar.

## 0.1.1 - 2026-11-24

- The first setup no longer waits for the address of the computer.
- The address counts as working after the first request that comes from the internet.
- Hermes and OpenClaw, once turned on, are open to every connected phone.
- A full uninstall leaves nothing behind.
- Refused requests are written to the log with a reason.
- The installer shows the progress of the download.
- The Linux preview is checked on a real server.

## 0.1.0 - 2026-11-24

- The first release.
- For a Mac with an Apple chip, installed with one line.
- Can also be installed by an AI agent.
- Works with Claude Code, Codex, Hermes and OpenClaw.
