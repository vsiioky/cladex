# Cladex

[English](README.md) | [Русский](README.ru.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Español](README.es.md) | [Italiano](README.it.md) | [简体中文](README.zh-Hans.md) | [繁體中文](README.zh-Hant.md) | **日本語** | [한국어](README.ko.md)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cladex)

Cladexは、ご自分のコンピュータで動くAIエージェントを、Even G2グラスに映して操作するリモコンです。

- AIエージェントが動く各コンピュータにプログラムをインス���ールします。専用のウィンドウを持つMacアプリです。
- グラス(スマートフォンのEvenアプリ経由)にエージェント、そのセッション、質問が表示され、タッチまたは音声で答えられます。
- すべて、スマートフォンからご自分のコンピュータへ、それぞれのアドレスで直接届きます。Cladexのサーバーもアカウントもありません。
- Claude Code、Codex、Hermes、OpenClawに対応しています。
- このリポジトリにあるのはビルドと手順書だけです。ソースコードは公開していません。

## AIエージェントでインストールする

このコンピュータのシェルを使えるAIエージェント(Claude Code、Codex、Hermes、OpenClawなど)をお使いなら、インストールをエージェントに任せられます。次の文をエージェントにコピーしてください。

```
Install Cladex on this computer. Read https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md and follow it step by step. Stop and ask me where it says so. Answer me in Japanese.
```

エージェントはこのリポジトリからCladexをダウンロードし、設定し、エージェントとスマートフォンを自動で接続します。ご本人にしか進められない場面では、止まって質問します。Tailscaleへのサインイン、コンピュータのアドレスをインターネットに公開すること(実行する前に確認���ます)、HermesとOpenClaw(ご本人の「はい」が必要です)、音声認識キー(チャットではなく、非表示の入力欄にご自分で入力します)、Claudeアプリでのディスパッチャ、そしてスマートフォンのコードです。管理者権限は一切使いません。

まず[AGENT-INSTALL.md](AGENT-INSTALL.md)をお読みください。短い文書で、エージェントがそのとおりに進めます。インターネットに接続できないエージェントには、アドレスの代わりにファイルそのものを渡せます。

## 必要なもの

- AppleチップのMac(M1以降)とmacOS 15以降。LinuxとWindowsはウィンドウのないプレビュー版です(「インストール」を参照)。IntelチップのMac向けのビルドはまだありません。
- 個人利用向けの無料のTailscaleアカウント(tailscale.com/download/mac)。コンピュータにインターネット上のアドレスを与えます。スマートフォン���Tailscaleをインストールする必要はありません。
- コンピュータにサインイン済みのAIエージェントが少なくとも1つ。Claude Code(claude.com/download)、Codex(developers.openai.com/codex/app)、Hermes(hermes-agent.nousresearch.com/docs/getting-started/installation)、OpenClaw(docs.openclaw.ai/install)のいずれかです。Claude Codeには有料のclaude.aiプランが必要です。
- Even G2グラスと、スマートフォンのEvenアプリ。

## インスト��ル

お使いのコンピュータを選んでください。それぞれ専用のコマンドと実行方法があります。

### AppleチップのMac(M1以降)

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

実行方法:

1. Cmd+Spaceを押し、「ターミナル」(Terminal)と入力してEnterを押します。文字を入力する行のあるウィンドウが開きます。
2. 上のコマンドをコピーし、そのウィンドウに貼り付���て(Cmd+V)Enterを押します。
3. 何をしたかが表示されるまで待ちます。スクリプトがパスワードを求めることはありません。

このあと表示されるもの: Cladexのウィンドウが開き、最初の設定を1ステップずつ案内します(下の節を参照)。

スクリプトの動作: ディスクイメージをダウンロードし、チェックサム、署名、Appleによる公証を確認し、Cladex.appを「アプリケーション」にコピーして、イメージを閉じ、Cladexを開きます。確認に通るまでは何も変更しません。/Applicationsに書き込めないときは、ホームフォルダのApplicationsフォルダを使い、その旨を表示します。Cladexが起動中なら、先に終了するよう求めます。オプション: `--no-open`、`--dir <folder>`、`--help`(行のあとに`| sh -s -- --no-open`のように付けます)。

手動でインストールする場合: https://github.com/vsiioky/cladex/releases を開き、cladex-arm64.dmgをダウンロードして開き、Cladexを「アプリケーション」にドラッグして、そこから開きます。同じページのSHA256SUMSでチェックサムを照合できます(`shasum -a 256 cladex-arm64.dmg`)。

状況: リリースの署名・公証済みディスクイメージで、実機のMacで動作を確認しています。

### IntelチップのMac

ビルドはまだありません。同じコマンドを実行すると、その旨を1文で表示し、何も変更せずに終了します。最新情報はリリースのページをご覧ください。

### Linux(x64とarm64)、プレビュー

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

実行方法:

1. ターミナルを開きます(多くのデスクトップではCtrl+Alt+T、またはプログラムのメニューで「ターミナル」を探します)。
2. 上のコマンドをコピーし、貼り付けて(Ctrl+Shift+V)Enterを押します。
3. 同じウィンドウに表示される質問に答えます。答えるまでは何も変更されません。

このあと表示されるもの: ウィンドウは開きません。スクリプトはCladexを~/.g2-claudeの下に置き、`cladex`コマンドをパスに追加して、`cladex setup`を起動します。質問はターミナルに表示されます。終わったら、次のコマンドを順に実行します。`cladex gateway init`、`cladex gateway publish`、`cladex pair`です(`cladex pair`はコンピュータのアドレスとコードを表示します)。インストールだけしたいときは、`| sh -s --`のあとに`--no-setup`を付けます。curl、tar、gzip、xz(パッケージxz-utils)が必要です。sudoは使わず、Node.js 22を自分でダウンロードしてチェックサムを確認します。

状況: プレビュー版です。Debianコンテナ(arm64)で、インストール、`cladex --version`、`cladex setup --print`をテストし��した。実機のLinuxコンピュータ、実際のサービス(systemd)、Tailscale、エージェントではテストしていません。

### Windows 10と11、プレビュー

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

実行方法:

1. スタートメニューを開き、PowerShellと入力してEnterを押します(「管理者として実行」ではなく、通常のウィンドウです)。
2. 上のコマンドをコピーし、貼り��けて(マウスの右クリックで貼り付けられます)Enterを押します。
3. 同じウィンドウに表示される質問に答えます。答えるまでは何も変更されません。

このあと表示されるもの: Cladexのウィンドウは開きません。スクリプトはCladexをユーザーフォルダの下(.g2-claude)に置き、コマンドのフォルダをユーザーのパスに追加して、`cladex setup`を起動します。質問はPowerShellに表示されます。���わったら、`cladex gateway init`、`cladex gateway publish`、`cladex pair`を順に実行します。インストールだけしたいときは、行の前に`$env:CLADEX_NO_SETUP = '1'`を設定します。管理者権限は使いません。

状況: プレビュー版です。スクリプトは目視と静的テストで確認しただけで、実機のWindowsではまだ実行していません。また、書いたマシンのPowerShellでは構文解析もしていません。

## 最初の設��

Macでは、Cladexのウィンドウが次のステップをそのつど示します。LinuxとWindowsでは、ターミナルの`cladex setup`と`cladex status`が示します。要点は次のとおりです。

1. Cladexを開きます。インストール計画を読み、1つだけの質問に答えます。答えるまでは何も変更されません。
2. Tailscale(tailscale.com/download/mac)をインストールして開き、サインインします。コンピュータの名前にご自分の���前が入っているときは、名前を変更します。
3. ブラウザでTailscaleのページを開きます。MagicDNSと「Enable HTTPS」をオンにし(console.tailscale.com/admin/dns)、ポリシーにFunnelを追加します(console.tailscale.com/admin/acls)。
4. Cladexで「アドレスを公開」を押し、コンピュータのアドレスを書き留めます。name.tailnet.ts.netのような形で、インターネット上に現れるまでに最長10分かかることがあります���
5. 上の一覧からAIエージェントをインストールし、サインインします。Cladexは他のプログラムをインストールせず、「もう一度確認」を押すとエージェントを自分で見つけます。Claude Codeの場合は、ウィンドウに一度だけのディスパッチャの手順も表示されます。
6. 音声入力は任意で、ElevenLabs(elevenlabs.io/app/settings/api-keys)かOpenAI(platform.openai.com/api-keys)のご自分のキーが必要です。Cladexの設定に貼り付けてください。

## グラス用アプリ

グラス用のCladexアプリは、Evenのベータチャンネルにあります。Evenがカタログに載せるまでは招待制で、招待はEvenアカウントのメールアドレスに送られます。招待を希望される場合は、このリポジトリ(https://github.com/vsiioky/cladex/issues)で「Beta invitation」というタイトルのissueを作成してください。issueは公開されるため、メール���ドレスは書かないでください。返信で、メールアドレスを非公開で送る方法をお伝えします。招待を受け取ったら、スマートフォンのEvenアプリでベータ版をインストールします。

## スマートフォンを接続する

1. コンピュータのCladexで「スマートフォンを接続」を押します。コンピュータのアドレスと8桁のコードが表示されます。
2. スマートフォンのEvenアプリの中のCladexアプ���で、アドレスとコードを入力し、続けてコンピュータに表示された3桁の数字を入力します。
3. グラスを装着します。「コンピュータがありません」と表示されたら、グラスの画面をタップします。一覧がもう一度確認されます。

## 更新

お使いのコンピュータ用のインストール行をもう一度実行します。Macでは、起動中のCladexを先に終了する必要があります。古いコピーは置き換えられます。設定とスマートフォンはそのまま残ります。

## 削除

Cladexで設定を開き、「削除」グループの「このコンピュータからCladexを削除...」を選びます。またはターミナルで`cladex uninstall`を実行します。Cladexがインストールしたものがすべて削除されます(サービス、フック、設定、キー、ログ)。そのあと、Cladex.appをゴミ箱に移します。Tailscaleとご利用のAIエージェント��残ります。

## プライバシー

- Cladexのサーバーもアカウントもありません。開発者がアプリやプログラムからデータを受け取ることはありません。
- 分析も、広告も、トラッキングもありません。
- 音声は、ご自分のコンピュータだけに送られ、そこからご自分のキーで音声認識サービスに送られます。

全文: [PRIVACY.md](PRIVACY.md)(英語)。利用条件: [TERMS.md](TERMS.md)(英語)。

## この��ロジェクトについて

Cladexのソースコードは公開していません。Cladexは独立したプロジェクトであり、Anthropic、OpenAI、Nous Research、OpenClaw、Even Realities、Tailscaleとは提携しておらず、これらの企業の承認も受けていません。製品名はそれぞれの所有者に帰属します。ご質問や問題は、このリポジトリのIssuesへお寄せください。

## Cladexを支援する

Cladexは無料で、これからも無料です��お役に立ちましたら、開発を支援していただけます: ko-fi.com/cladex。
