# Cladex

[English](README.md) | [Русский](README.ru.md) | [Deutsch](README.de.md) | **Français** | [Español](README.es.md) | [Italiano](README.it.md) | [简体中文](README.zh-Hans.md) | [繁體中文](README.zh-Hant.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cladex)

Cladex est une télécommande pour les agents d’IA qui travaillent sur vos propres ordinateurs, affichée sur les lunettes Even G2.

- Vous installez un programme sur chaque ordinateur où travaillent vos agents d’IA. C’est une application Mac avec sa propre fenêtre.
- Les lunettes (via l’application Even sur votre téléphone) montrent vos agents, leurs sessions et leurs questions, et vous laissent répondre au toucher ou à la voix.
- Tout va de votre téléphone vers vos propres ordinateurs, par leurs propres adresses. Il n’y a ni serveur Cladex ni compte Cladex.
- Fonctionne avec Claude Code, Codex, Hermes et OpenClaw.
- Ce dépôt ne contient que les versions compilées et les instructions. Le code source n’est pas publié.

## Installer avec votre agent d’IA

Si vous travaillez avec un agent d’IA qui dispose d’un terminal sur cet ordinateur (Claude Code, Codex, Hermes, OpenClaw ou un autre), vous pouvez lui confier l’installation. Copiez ce texte dans l’agent :

```
Installe Cladex sur cet ordinateur. Lis https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md et suis-le pas à pas. Arrête-toi et demande-moi là où c’est indiqué. Réponds-moi en français.
```

L’agent télécharge Cladex depuis ce dépôt, le configure et connecte lui-même vos agents et votre téléphone. Il s’arrête et vous demande là où vous seul pouvez continuer : la connexion à Tailscale, l’ouverture de l’adresse de l’ordinateur sur Internet (il demande avant de le faire), Hermes et OpenClaw (ils ont besoin de votre accord), une clé de reconnaissance vocale (vous la saisissez à une invite masquée, jamais dans la conversation), le répartiteur Claude dans l’application Claude, et le code sur votre téléphone. Il n’utilise jamais de droits d’administrateur.

Lisez d’abord [AGENT-INSTALL.md](AGENT-INSTALL.md) : il est court, et c’est exactement ce que l’agent suivra. À un agent sans accès à Internet, vous pouvez donner le fichier lui-même au lieu de l’adresse.

## Ce qu’il vous faut

- Un Mac avec une puce Apple (M1 ou plus récent) et macOS 15 ou plus récent. Linux et Windows sont un aperçu sans fenêtre (voir Installation) ; il n’y a pas encore de version pour un Mac avec une puce Intel.
- Un compte Tailscale gratuit pour un usage personnel (tailscale.com/download/mac). Il donne à l’ordinateur une adresse sur Internet. Vous n’installez pas Tailscale sur le téléphone.
- Au moins un agent d’IA sur l’ordinateur, où vous êtes connecté : Claude Code (claude.com/download), Codex (developers.openai.com/codex/app), Hermes (hermes-agent.nousresearch.com/docs/getting-started/installation) ou OpenClaw (docs.openclaw.ai/install). Claude Code demande une offre payante de claude.ai.
- Les lunettes Even G2 et l’application Even sur votre téléphone.

## Installation

Choisissez votre ordinateur. Chacun a sa propre commande et sa propre façon de l’exécuter.

### Mac avec une puce Apple (M1 ou plus récent)

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

Comment l’exécuter :

1. Appuyez sur Cmd+Espace, tapez Terminal et appuyez sur Entrée. Une fenêtre avec une ligne de texte s’ouvre.
2. Copiez la commande ci-dessus, collez-la dans cette fenêtre (Cmd+V) et appuyez sur Entrée.
3. Attendez qu’il indique ce qu’il a fait. Le script ne demande jamais votre mot de passe.

Ce que vous voyez ensuite : la fenêtre de Cladex s’ouvre et vous guide dans la première configuration, une étape à la fois (la section ci-dessous).

Ce que fait le script : il télécharge l’image disque, vérifie sa somme de contrôle, sa signature et sa notarisation par Apple, copie Cladex.app dans Applications, éjecte l’image et ouvre Cladex. Il ne change rien tant que les vérifications ne sont pas réussies. Si /Applications n’est pas accessible en écriture, il utilise le dossier Applications de votre dossier personnel et le dit. Si Cladex est en cours d’exécution, il vous demande de le quitter d’abord. Options : `--no-open`, `--dir <folder>`, `--help` (après la ligne : `| sh -s -- --no-open`).

À la main : ouvrez https://github.com/vsiioky/cladex/releases, téléchargez cladex-arm64.dmg, ouvrez-le, glissez Cladex dans Applications et ouvrez-le de là. La même page contient SHA256SUMS pour comparer la somme de contrôle (`shasum -a 256 cladex-arm64.dmg`).

Statut : vérifié sur un vrai Mac avec l’image disque signée et notarisée de la version.

### Mac avec une puce Intel

Il n’y a pas encore de version. La même commande le dit en une phrase et s’arrête sans rien changer. Consultez la page des versions pour les nouveautés.

### Linux (x64 et arm64), aperçu

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

Comment l’exécuter :

1. Ouvrez un terminal (sur la plupart des bureaux : Ctrl+Alt+T, ou cherchez « Terminal » dans le menu des applications).
2. Copiez la commande ci-dessus, collez-la (Ctrl+Maj+V) et appuyez sur Entrée.
3. Répondez aux questions qui apparaissent dans la même fenêtre. Rien ne change tant que vous n’avez pas répondu.

Ce que vous voyez ensuite : pas de fenêtre. Le script place Cladex sous ~/.g2-claude, met la commande `cladex` dans votre chemin et lance `cladex setup`, qui pose ses questions dans le terminal. Quand il a fini, exécutez ces commandes l’une après l’autre : `cladex gateway init`, puis `cladex gateway publish`, puis `cladex pair` (elle affiche l’adresse de l’ordinateur et un code). Ajoutez `--no-setup` après `| sh -s --` pour seulement installer. Il faut curl, tar, gzip et xz (le paquet xz-utils) ; le script n’utilise jamais sudo, télécharge lui-même Node.js 22 et vérifie sa somme de contrôle.

Statut : aperçu. Testé dans un conteneur Debian (arm64) : l’installation, `cladex --version` et `cladex setup --print`. Non testé sur un vrai ordinateur Linux, avec de vrais services (systemd), Tailscale ou des agents.

### Windows 10 et 11, aperçu

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

Comment l’exécuter :

1. Ouvrez le menu Démarrer, tapez PowerShell et appuyez sur Entrée (une fenêtre ordinaire, pas « en tant qu’administrateur »).
2. Copiez la commande ci-dessus, collez-la (un clic droit colle) et appuyez sur Entrée.
3. Répondez aux questions qui apparaissent dans la même fenêtre. Rien ne change tant que vous n’avez pas répondu.

Ce que vous voyez ensuite : pas de fenêtre de Cladex. Le script place Cladex sous votre dossier utilisateur (.g2-claude), ajoute son dossier de commandes au chemin de votre utilisateur et lance `cladex setup`, qui pose ses questions dans PowerShell. Quand il a fini, exécutez : `cladex gateway init`, puis `cladex gateway publish`, puis `cladex pair`. Pour seulement installer, définissez `$env:CLADEX_NO_SETUP = '1'` avant la ligne. Aucun droit d’administrateur n’est utilisé.

Statut : aperçu. Le script a seulement été relu et vérifié à la main et par des tests statiques : il n’a pas encore été exécuté sur un vrai ordinateur Windows, et PowerShell ne l’a pas analysé sur la machine où il a été écrit.

## La première configuration

Sur un Mac, Cladex nomme chaque étape suivante dans sa fenêtre ; sous Linux et Windows, `cladex setup` et `cladex status` les nomment dans le terminal. En bref :

1. Ouvrez Cladex. Lisez le plan d’installation et répondez à sa seule question. Rien ne change tant que vous n’avez pas répondu.
2. Installez Tailscale (tailscale.com/download/mac), ouvrez-le et connectez-vous. Renommez l’ordinateur si son nom contient votre propre nom.
3. Dans les pages de Tailscale, dans un navigateur : activez MagicDNS et « Enable HTTPS » (console.tailscale.com/admin/dns) et ajoutez Funnel à la politique (console.tailscale.com/admin/acls).
4. Dans Cladex, cliquez sur « Publier l’adresse » et notez l’adresse de l’ordinateur. Elle ressemble à name.tailnet.ts.net et peut mettre jusqu’à 10 minutes à apparaître sur Internet.
5. Installez un agent d’IA de la liste ci-dessus et connectez-vous. Cladex n’installe pas d’autres programmes et trouve l’agent lui-même après « Vérifier à nouveau ». Pour Claude Code, la fenêtre montre aussi une étape unique du répartiteur.
6. La voix est facultative et demande votre propre clé ElevenLabs (elevenlabs.io/app/settings/api-keys) ou OpenAI (platform.openai.com/api-keys). Collez-la dans Cladex, Réglages.

## L’application pour les lunettes

L’application Cladex pour les lunettes est dans le canal bêta d’Even. Elle n’y est que sur invitation, jusqu’à ce qu’Even la liste dans son catalogue, et l’invitation est envoyée à l’adresse e-mail de votre compte Even. Pour en demander une, ouvrez un ticket (issue) dans ce dépôt (https://github.com/vsiioky/cladex/issues) avec le titre « Beta invitation ». N’écrivez pas votre adresse e-mail dans le ticket : un ticket est public, et la réponse vous dira comment envoyer l’adresse e-mail en privé. Après l’invitation, installez la version bêta dans l’application Even sur votre téléphone.

## Connecter le téléphone

1. Dans Cladex sur l’ordinateur, cliquez sur « Connecter un téléphone » : l’adresse de l’ordinateur et un code à 8 chiffres apparaissent.
2. Dans l’application Cladex, dans l’application Even sur le téléphone, saisissez l’adresse et le code, puis les 3 chiffres affichés sur l’ordinateur.
3. Mettez les lunettes. Si elles disent « Aucun ordinateur », touchez l’écran des lunettes : la liste est revérifiée.

## Mise à jour

Exécutez de nouveau la ligne d’installation de votre ordinateur : sur un Mac, un Cladex en cours d’exécution doit d’abord être quitté, et l’ancienne copie est remplacée. Vos réglages et vos téléphones restent.

## Suppression

Dans Cladex, ouvrez Réglages, le groupe « Suppression », « Supprimer Cladex de cet ordinateur... ». Ou, dans le Terminal, exécutez `cladex uninstall` : il supprime tout ce que Cladex a installé (le service, les hooks, les réglages, les clés, les journaux). Mettez ensuite Cladex.app à la Corbeille. Tailscale et vos agents d’IA restent.

## Confidentialité

- Il n’y a ni serveur Cladex ni compte. Le développeur ne reçoit aucune donnée de l’application ni du programme.
- Pas d’analyse d’audience, pas de publicité, pas de pistage.
- Votre voix va seulement à votre propre ordinateur, et de là au service de reconnaissance vocale avec votre propre clé.

Texte complet : [PRIVACY.md](PRIVACY.md) (en anglais). Conditions d’utilisation : [TERMS.md](TERMS.md) (en anglais).

## À propos

Le code source de Cladex n’est pas publié. Cladex est indépendant et n’est ni affilié à Anthropic, OpenAI, Nous Research, OpenClaw, Even Realities ou Tailscale, ni approuvé par eux. Les noms de produits appartiennent à leurs propriétaires. Questions et problèmes : les Issues de ce dépôt.

## Soutenir Cladex

Cladex est gratuit et le restera. S’il vous aide, vous pouvez soutenir son développement : ko-fi.com/cladex.
