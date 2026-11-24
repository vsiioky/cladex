# Cladex

[English](README.md) | [Русский](README.ru.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Español](README.es.md) | **Italiano** | [简体中文](README.zh-Hans.md) | [繁體中文](README.zh-Hant.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cladex)

Cladex è un telecomando per gli agenti IA che lavorano sui Suoi computer, mostrato sugli occhiali Even G2.

- Lei installa un programma su ogni computer dove lavorano i Suoi agenti IA. È un'app per Mac con una propria finestra.
- Gli occhiali (tramite l'app Even sul Suo telefono) mostrano i Suoi agenti, le loro sessioni e le loro domande, e Le permettono di rispondere con il tocco o con la voce.
- Tutto va dal Suo telefono ai Suoi computer, tramite i loro indirizzi. Non esistono un server Cladex né un account Cladex.
- Funziona con Claude Code, Codex, Hermes e OpenClaw.
- Questo repository contiene solo le build e le istruzioni. Il codice sorgente non è pubblicato.

## Installare con il Suo agente IA

Se lavora con un agente IA che ha una shell su questo computer (Claude Code, Codex, Hermes, OpenClaw o un altro), può affidargli l'installazione. Copi questo testo nell'agente:

```
Installa Cladex su questo computer. Leggi https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md e seguilo passo dopo passo. Fermati e chiedimi dove è indicato. Rispondimi in italiano.
```

L'agente scarica Cladex da questo repository, lo configura e collega da solo i Suoi agenti e il Suo telefono. Si ferma e Le chiede dove solo Lei può proseguire: l'accesso a Tailscale, l'apertura dell'indirizzo del computer a Internet (chiede prima di farlo), Hermes e OpenClaw (serve il Suo consenso), una chiave per il riconoscimento vocale (la inserisce Lei a un prompt nascosto, mai nella chat), il dispatcher di Claude nell'app Claude e il codice sul Suo telefono. Non usa mai i diritti di amministratore.

Legga prima [AGENT-INSTALL.md](AGENT-INSTALL.md): è breve ed è esattamente ciò che l'agente seguirà. A un agente senza accesso a Internet si può dare il file stesso al posto dell'indirizzo.

## Cosa serve

- Un Mac con chip Apple (M1 o successivo) e macOS 15 o successivo. Linux e Windows sono un'anteprima senza finestra (vedi Installazione); per un Mac con chip Intel non c'è ancora una build.
- Un account Tailscale gratuito per uso personale (tailscale.com/download/mac). Dà al computer un indirizzo su Internet. Non deve installare Tailscale sul telefono.
- Almeno un agente IA sul computer, con l'accesso già effettuato: Claude Code (claude.com/download), Codex (developers.openai.com/codex/app), Hermes (hermes-agent.nousresearch.com/docs/getting-started/installation) oppure OpenClaw (docs.openclaw.ai/install). Claude Code richiede un piano a pagamento di claude.ai.
- Gli occhiali Even G2 e l'app Even sul Suo telefono.

## Installazione

Scelga il Suo computer. Ognuno ha il proprio comando e il proprio modo di eseguirlo.

### Mac con chip Apple (M1 o successivo)

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

Come eseguirlo:

1. Prema Cmd+Spazio, scriva Terminale e prema Invio. Si apre una finestra con una riga di testo.
2. Copi il comando qui sopra, lo incolli in quella finestra (Cmd+V) e prema Invio.
3. Attenda finché non dice cosa ha fatto. Lo script non chiede mai la Sua password.

Cosa vedrà dopo: si apre la finestra di Cladex e La guida nella prima configurazione, un passaggio alla volta (la sezione qui sotto).

Cosa fa lo script: scarica l'immagine disco, ne controlla la checksum, la firma e la notarizzazione da parte di Apple, copia Cladex.app in Applicazioni, espelle l'immagine e apre Cladex. Non cambia nulla finché i controlli non sono superati. Se /Applications non è scrivibile, usa la cartella Applicazioni nella Sua cartella home e lo dice. Se Cladex è in esecuzione, Le chiede di chiuderlo prima. Opzioni: `--no-open`, `--dir <folder>`, `--help` (dopo la riga: `| sh -s -- --no-open`).

A mano: apra https://github.com/vsiioky/cladex/releases, scarichi cladex-arm64.dmg, lo apra, trascini Cladex in Applicazioni e lo apra da lì. La stessa pagina contiene SHA256SUMS per confrontare la checksum (`shasum -a 256 cladex-arm64.dmg`).

Stato: verificato su un Mac reale con l'immagine disco firmata e notarizzata della versione.

### Mac con chip Intel

Non c'è ancora una build. Lo stesso comando lo dice in una frase e si ferma senza cambiare nulla. Guardi la pagina delle versioni per le novità.

### Linux (x64 e arm64), anteprima

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

Come eseguirlo:

1. Apra un terminale (sulla maggior parte dei desktop: Ctrl+Alt+T, oppure cerchi "Terminale" nel menu delle applicazioni).
2. Copi il comando qui sopra, lo incolli (Ctrl+Maiusc+V) e prema Invio.
3. Risponda alle domande che compaiono nella stessa finestra. Non cambia nulla finché non risponde.

Cosa vedrà dopo: nessuna finestra. Lo script mette Cladex in ~/.g2-claude, mette il comando `cladex` nel Suo percorso e avvia `cladex setup`, che fa le sue domande nel terminale. Quando ha finito, esegua questi comandi uno dopo l'altro: `cladex gateway init`, poi `cladex gateway publish`, poi `cladex pair` (stampa l'indirizzo del computer e un codice). Aggiunga `--no-setup` dopo `| sh -s --` per installare soltanto. Servono curl, tar, gzip e xz (il pacchetto xz-utils); lo script non usa mai sudo, scarica da solo Node.js 22 e ne controlla la checksum.

Stato: anteprima. Provato in un container Debian (arm64): l'installazione, `cladex --version` e `cladex setup --print`. Non provato su un computer Linux reale, con servizi reali (systemd), con Tailscale o con agenti.

### Windows 10 e 11, anteprima

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

Come eseguirlo:

1. Apra il menu Start, scriva PowerShell e prema Invio (una finestra normale, non "come amministratore").
2. Copi il comando qui sopra, lo incolli (il clic destro incolla) e prema Invio.
3. Risponda alle domande che compaiono nella stessa finestra. Non cambia nulla finché non risponde.

Cosa vedrà dopo: nessuna finestra di Cladex. Lo script mette Cladex nella Sua cartella utente (.g2-claude), aggiunge la sua cartella dei comandi al percorso del Suo utente e avvia `cladex setup`, che fa le sue domande in PowerShell. Quando ha finito, esegua: `cladex gateway init`, poi `cladex gateway publish`, poi `cladex pair`. Per installare soltanto, imposti `$env:CLADEX_NO_SETUP = '1'` prima della riga. Non vengono usati diritti di amministratore.

Stato: anteprima. Lo script è stato solo letto e controllato a mano e con test statici: non è ancora stato eseguito su un computer Windows reale, e PowerShell non l'ha analizzato sulla macchina dove è stato scritto.

## La prima configurazione

Su un Mac, Cladex indica ogni passaggio successivo nella sua finestra; su Linux e Windows lo indicano `cladex setup` e `cladex status` nel terminale. In breve:

1. Apra Cladex. Legga il piano di installazione e risponda alla sua unica domanda. Non cambia nulla finché non risponde.
2. Installi Tailscale (tailscale.com/download/mac), lo apra ed effettui l'accesso. Rinomini il computer se il suo nome contiene il Suo nome.
3. Nelle pagine di Tailscale, in un browser: attivi MagicDNS e "Enable HTTPS" (console.tailscale.com/admin/dns) e aggiunga Funnel alla policy (console.tailscale.com/admin/acls).
4. In Cladex faccia clic su "Pubblica indirizzo" e annoti l'indirizzo del computer. Ha l'aspetto name.tailnet.ts.net e può impiegare fino a 10 minuti per comparire su Internet.
5. Installi un agente IA dell'elenco qui sopra e acceda. Cladex non installa altri programmi e trova da solo l'agente dopo "Controlla di nuovo". Per Claude Code la finestra mostra anche un passaggio una tantum del dispatcher.
6. La voce è facoltativa e richiede una Sua chiave personale di ElevenLabs (elevenlabs.io/app/settings/api-keys) o di OpenAI (platform.openai.com/api-keys). La incolli in Cladex, Impostazioni.

## L'app per gli occhiali

L'app Cladex per gli occhiali è nel canale beta di Even. È lì solo su invito finché Even non la inserisce nel suo catalogo, e l'invito viene inviato all'e-mail del Suo account Even. Per richiederne uno, apra una issue in questo repository (https://github.com/vsiioky/cladex/issues) con il titolo "Beta invitation". Non scriva la Sua e-mail nella issue: una issue è pubblica, e la risposta Le dirà come inviare l'e-mail in privato. Dopo l'invito, installi la build beta nell'app Even sul Suo telefono.

## Collegare il telefono

1. In Cladex sul computer faccia clic su "Collega il telefono": compaiono l'indirizzo del computer e un codice di 8 cifre.
2. Nell'app Cladex dentro l'app Even sul telefono inserisca l'indirizzo e il codice, poi le 3 cifre mostrate sul computer.
3. Indossi gli occhiali. Se dicono "Nessun computer", tocchi lo schermo degli occhiali: l'elenco viene ricontrollato.

## Aggiornamento

Esegua di nuovo la riga di installazione del Suo computer: su un Mac un Cladex in esecuzione va chiuso prima, e la copia più vecchia viene sostituita. Le Sue impostazioni e i Suoi telefoni restano.

## Rimozione

In Cladex apra Impostazioni, il gruppo "Rimozione", "Rimuovi Cladex da questo computer...". Oppure nel Terminale esegua `cladex uninstall`: rimuove tutto ciò che Cladex ha installato (il servizio, gli hook, le impostazioni, le chiavi, i registri). Poi sposti Cladex.app nel Cestino. Tailscale e i Suoi agenti IA restano.

## Privacy

- Non esistono un server Cladex né un account. Lo sviluppatore non riceve alcun dato dall'app né dal programma.
- Nessuna analisi, nessuna pubblicità, nessun tracciamento.
- La Sua voce va solo al Suo computer e da lì al servizio di riconoscimento vocale con la Sua chiave personale.

Testo completo: [PRIVACY.md](PRIVACY.md) (in inglese). Condizioni d'uso: [TERMS.md](TERMS.md) (in inglese).

## Informazioni

Il codice sorgente di Cladex non è pubblicato. Cladex è indipendente e non è affiliato né approvato da Anthropic, OpenAI, Nous Research, OpenClaw, Even Realities o Tailscale. I nomi dei prodotti appartengono ai rispettivi proprietari. Domande e problemi: le Issues di questo repository.

## Sostenere Cladex

Cladex è gratuito e lo resterà. Se Le è utile, può sostenerne lo sviluppo: ko-fi.com/cladex.
