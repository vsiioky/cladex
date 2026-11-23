# Cladex

[English](README.md) | [Русский](README.ru.md) | **Deutsch** | [Français](README.fr.md) | [Español](README.es.md) | [Italiano](README.it.md) | [简体中文](README.zh-Hans.md) | [繁體中文](README.zh-Hant.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

Cladex ist eine Fernbedienung für die KI-Agenten, die auf Ihren eigenen Computern arbeiten, angezeigt auf der Even G2 Brille.

- Sie installieren ein Programm auf jedem Computer, auf dem Ihre KI-Agenten arbeiten. Es ist eine Mac-App mit eigenem Fenster.
- Die Brille (über die Even-App auf Ihrem Telefon) zeigt Ihre Agenten, ihre Sessions und ihre Fragen und lässt Sie per Touch oder per Sprache antworten.
- Alles läuft von Ihrem Telefon zu Ihren eigenen Computern, über deren eigene Adressen. Es gibt keinen Cladex-Server und kein Cladex-Konto.
- Funktioniert mit Claude Code, Codex, Hermes und OpenClaw.
- Dieses Repository enthält nur die Builds und die Anleitungen. Der Quellcode ist nicht veröffentlicht.

## Installation mit Ihrem KI-Agenten

Wenn Sie mit einem KI-Agenten arbeiten, der auf diesem Computer eine Shell hat (Claude Code, Codex, Hermes, OpenClaw oder einem anderen), können Sie ihm die Installation überlassen. Kopieren Sie diesen Text in den Agenten:

```
Installiere Cladex auf diesem Computer. Lies https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md und befolge es Schritt für Schritt. Halte an und frage mich, wo es dort steht. Antworte mir auf Deutsch.
```

Der Agent lädt Cladex aus diesem Repository herunter, richtet es ein und verbindet Ihre Agenten und Ihr Telefon selbst. Er hält an und fragt Sie dort, wo nur Sie weitermachen können: Anmeldung bei Tailscale, Freigabe der Adresse des Computers im Internet (er fragt, bevor er es tut), Hermes und OpenClaw (sie brauchen Ihr Ja), ein Schlüssel für die Spracherkennung (Sie geben ihn an einer verdeckten Eingabeaufforderung ein, nie im Chat), der Claude-Dispatcher in der Claude-App und der Code auf Ihrem Telefon. Er verwendet nie Administratorrechte.

Lesen Sie zuerst [AGENT-INSTALL.md](AGENT-INSTALL.md): Die Datei ist kurz und genau das, was der Agent befolgen wird. Einem Agenten ohne Internetzugang können Sie statt der Adresse die Datei selbst geben.

## Was Sie brauchen

- Einen Mac mit Apple-Chip (M1 oder neuer) und macOS 15 oder neuer. Linux und Windows sind eine Vorschau ohne Fenster (siehe Installation); für einen Mac mit Intel-Chip gibt es noch keinen Build.
- Ein kostenloses Tailscale-Konto für den privaten Gebrauch (tailscale.com/download/mac). Es gibt dem Computer eine Adresse im Internet. Tailscale müssen Sie auf dem Telefon nicht installieren.
- Mindestens einen KI-Agenten auf dem Computer, bei dem Sie angemeldet sind: Claude Code (claude.com/download), Codex (developers.openai.com/codex/app), Hermes (hermes-agent.nousresearch.com/docs/getting-started/installation) oder OpenClaw (docs.openclaw.ai/install). Claude Code braucht einen bezahlten claude.ai-Tarif.
- Die Even G2 Brille und die Even-App auf Ihrem Telefon.

## Installation

Wählen Sie Ihren Computer. Jeder hat seinen eigenen Befehl und seine eigene Art, ihn auszuführen.

### Mac mit Apple-Chip (M1 oder neuer)

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

So führen Sie ihn aus:

1. Drücken Sie Cmd+Leertaste, tippen Sie Terminal und drücken Sie die Eingabetaste. Es öffnet sich ein Fenster mit einer Textzeile.
2. Kopieren Sie den Befehl oben, fügen Sie ihn in dieses Fenster ein (Cmd+V) und drücken Sie die Eingabetaste.
3. Warten Sie, bis gemeldet wird, was erledigt wurde. Das Skript fragt nie nach Ihrem Passwort.

Was Sie danach sehen: Das Cladex-Fenster öffnet sich und führt Sie Schritt für Schritt durch die erste Einrichtung (der Abschnitt unten).

Was das Skript tut: Es lädt das Festplattenabbild herunter, prüft dessen Prüfsumme, dessen Signatur und dessen Notarisierung durch Apple, kopiert Cladex.app in Programme, wirft das Abbild aus und öffnet Cladex. Bis die Prüfungen bestanden sind, ändert es nichts. Wenn /Applications nicht beschreibbar ist, nimmt es den Ordner Programme in Ihrem Home-Ordner und sagt das. Läuft Cladex gerade, bittet es Sie, das Programm zuerst zu beenden. Optionen: `--no-open`, `--dir <folder>`, `--help` (nach der Zeile: `| sh -s -- --no-open`).

Von Hand: Öffnen Sie https://github.com/vsiioky/cladex/releases, laden Sie cladex-arm64.dmg herunter, öffnen Sie die Datei, ziehen Sie Cladex in Programme und öffnen Sie es von dort. Auf derselben Seite liegt SHA256SUMS zum Vergleich der Prüfsumme (`shasum -a 256 cladex-arm64.dmg`).

Status: geprüft auf einem echten Mac mit dem signierten und notarisierten Festplattenabbild des Releases.

### Mac mit Intel-Chip

Dafür gibt es noch keinen Build. Derselbe Befehl sagt das in einem Satz und hält an, ohne etwas zu ändern. Neuigkeiten finden Sie auf der Seite der Releases.

### Linux (x64 und arm64), Vorschau

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

So führen Sie ihn aus:

1. Öffnen Sie ein Terminal (auf den meisten Oberflächen: Strg+Alt+T, oder suchen Sie „Terminal“ im Programmmenü).
2. Kopieren Sie den Befehl oben, fügen Sie ihn ein (Strg+Umschalt+V) und drücken Sie die Eingabetaste.
3. Beantworten Sie die Fragen, die im selben Fenster erscheinen. Bis Sie antworten, ändert sich nichts.

Was Sie danach sehen: kein Fenster. Das Skript legt Cladex unter ~/.g2-claude ab, legt den Befehl `cladex` in Ihren Pfad und startet `cladex setup`, das seine Fragen im Terminal stellt. Wenn es fertig ist, führen Sie diese Befehle nacheinander aus: `cladex gateway init`, dann `cladex gateway publish`, dann `cladex pair` (er gibt die Adresse des Computers und einen Code aus). Fügen Sie `--no-setup` nach `| sh -s --` an, um nur zu installieren. Es braucht curl, tar, gzip und xz (das Paket xz-utils), verwendet nie sudo und lädt Node.js 22 selbst herunter und prüft dessen Prüfsumme.

Status: Vorschau. Getestet in einem Debian-Container (arm64): die Installation, `cladex --version` und `cladex setup --print`. Nicht getestet auf einem echten Linux-Computer, mit echten Diensten (systemd), mit Tailscale oder mit Agenten.

### Windows 10 und 11, Vorschau

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

So führen Sie ihn aus:

1. Öffnen Sie das Startmenü, tippen Sie PowerShell und drücken Sie die Eingabetaste (ein gewöhnliches Fenster, nicht „als Administrator“).
2. Kopieren Sie den Befehl oben, fügen Sie ihn ein (ein Klick mit der rechten Maustaste fügt ein) und drücken Sie die Eingabetaste.
3. Beantworten Sie die Fragen, die im selben Fenster erscheinen. Bis Sie antworten, ändert sich nichts.

Was Sie danach sehen: kein Cladex-Fenster. Das Skript legt Cladex unter Ihrem Benutzerordner (.g2-claude) ab, fügt dessen Befehlsordner dem Pfad Ihres Benutzers hinzu und startet `cladex setup`, das seine Fragen in PowerShell stellt. Wenn es fertig ist, führen Sie aus: `cladex gateway init`, dann `cladex gateway publish`, dann `cladex pair`. Um nur zu installieren, setzen Sie vor der Zeile `$env:CLADEX_NO_SETUP = '1'`. Es werden keine Administratorrechte verwendet.

Status: Vorschau. Das Skript wurde nur von Hand und durch statische Tests gelesen und geprüft: Es wurde noch nicht auf einem echten Windows-Computer ausgeführt, und PowerShell hat es auf dem Rechner, auf dem es geschrieben wurde, nicht geparst.

## Die Ersteinrichtung

Auf dem Mac nennt Cladex jeden nächsten Schritt in seinem Fenster; unter Linux und Windows nennen ihn `cladex setup` und `cladex status` im Terminal. Kurz gesagt:

1. Öffnen Sie Cladex. Lesen Sie den Installationsplan und beantworten Sie dessen einzige Frage. Bis Sie antworten, ändert sich nichts.
2. Installieren Sie Tailscale (tailscale.com/download/mac), öffnen Sie es und melden Sie sich an. Benennen Sie den Computer um, wenn sein Name Ihren eigenen Namen enthält.
3. Auf den Seiten von Tailscale, in einem Browser: Schalten Sie MagicDNS und „Enable HTTPS“ ein (console.tailscale.com/admin/dns) und fügen Sie Funnel zur Richtlinie hinzu (console.tailscale.com/admin/acls).
4. Klicken Sie in Cladex auf „Adresse veröffentlichen“ und notieren Sie sich die Adresse des Computers. Sie sieht aus wie name.tailnet.ts.net und kann bis zu 10 Minuten brauchen, bis sie im Internet erscheint.
5. Installieren Sie einen KI-Agenten aus der Liste oben und melden Sie sich bei ihm an. Cladex installiert keine anderen Programme und findet den Agenten nach „Erneut prüfen“ selbst. Bei Claude Code zeigt das Fenster außerdem einen einmaligen Dispatcher-Schritt.
6. Die Spracheingabe ist optional und braucht Ihren eigenen Schlüssel von ElevenLabs (elevenlabs.io/app/settings/api-keys) oder OpenAI (platform.openai.com/api-keys). Fügen Sie ihn in Cladex unter Einstellungen ein.

## Die App für die Brille

Die Cladex-App für die Brille ist im Beta-Kanal von Even. Sie ist dort nur auf Einladung verfügbar, bis Even sie in seinen Katalog aufnimmt, und die Einladung geht an die E-Mail-Adresse Ihres Even-Kontos. Um eine anzufordern, eröffnen Sie in diesem Repository ein Issue (https://github.com/vsiioky/cladex/issues) mit dem Titel „Beta invitation“. Schreiben Sie Ihre E-Mail-Adresse nicht in das Issue: Ein Issue ist öffentlich, und die Antwort sagt Ihnen, wie Sie die E-Mail-Adresse privat senden. Nach der Einladung installieren Sie den Beta-Build in der Even-App auf Ihrem Telefon.

## Das Telefon verbinden

1. Klicken Sie in Cladex auf dem Computer auf „Telefon verbinden“: Die Adresse des Computers und ein 8-stelliger Code erscheinen.
2. Geben Sie in der Cladex-App in der Even-App auf dem Telefon die Adresse und den Code ein, dann die 3 Ziffern, die auf dem Computer angezeigt werden.
3. Setzen Sie die Brille auf. Zeigt sie „Keine Computer“, tippen Sie auf den Bildschirm der Brille: Die Liste wird erneut geprüft.

## Update

Führen Sie die Installationszeile Ihres Computers erneut aus: Auf dem Mac muss ein laufendes Cladex zuerst beendet werden, und die ältere Kopie wird ersetzt. Ihre Einstellungen und Ihre Telefone bleiben erhalten.

## Entfernen

Öffnen Sie in Cladex die Einstellungen, die Gruppe „Entfernen“, „Cladex von diesem Computer entfernen ...“. Oder führen Sie im Terminal `cladex uninstall` aus: Es entfernt alles, was Cladex installiert hat (den Dienst, die Hooks, die Einstellungen, die Schlüssel, die Protokolle). Ziehen Sie dann Cladex.app in den Papierkorb. Tailscale und Ihre KI-Agenten bleiben.

## Datenschutz

- Es gibt keinen Cladex-Server und kein Konto. Der Entwickler erhält keine Daten von der App oder vom Programm.
- Keine Analyse, keine Werbung, kein Tracking.
- Ihre Stimme geht nur an Ihren eigenen Computer und von dort mit Ihrem eigenen Schlüssel an den Spracherkennungsdienst.

Vollständiger Text: [PRIVACY.md](PRIVACY.md) (auf Englisch). Nutzungsbedingungen: [TERMS.md](TERMS.md) (auf Englisch).

## Über das Projekt

Der Quellcode von Cladex ist nicht veröffentlicht. Cladex ist unabhängig und steht in keiner Verbindung zu Anthropic, OpenAI, Nous Research, OpenClaw, Even Realities oder Tailscale und wird von ihnen nicht unterstützt. Produktnamen gehören ihren Inhabern. Fragen und Probleme: die Issues dieses Repositorys.

## Cladex unterstützen

Cladex ist kostenlos und bleibt es. Wenn es Ihnen hilft, können Sie seine Entwicklung unterstützen: ko-fi.com/cladex.
