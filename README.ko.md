# Cladex

[English](README.md) | [Русский](README.ru.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Español](README.es.md) | [Italiano](README.it.md) | [简体中文](README.zh-Hans.md) | [繁體中文](README.zh-Hant.md) | [日本語](README.ja.md) | **한국어**

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cladex)

Cladex는 내 컴퓨터에서 일하는 AI 에이전트를 Even G2 안경으로 보면서 조작하는 리모컨이에요.

- AI 에이전트가 일하는 컴퓨터마다 프로그램을 설치해요. 자체 창이 있는 Mac 앱이에요.
- 안경(휴대폰의 Even 앱을 거쳐요)에 에이전트와 세션, 질문이 보이고, 터치나 음성으로 답할 수 있어요.
- 모든 것은 휴대폰에서 내 컴퓨터로, 각 컴퓨터의 주소로 곧바로 가요. Cladex 서버도 Cladex 계정도 없어요.
- Claude Code, Codex, Hermes, OpenClaw와 함께 작동해요.
- 이 저장소에는 빌드와 안내만 있어요. 소스 코드는 공개하지 않아요.

## AI 에이전트로 설치하기

이 컴퓨터에서 셸을 쓸 수 있는 AI 에이전트(Claude Code, Codex, Hermes, OpenClaw 또는 다른 에이전트)를 쓰고 있다면 설치를 에이전트에게 맡길 수 있어요. 아래 글을 에이전트에게 복사해 주세요.

```
Install Cladex on this computer. Read https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md and follow it step by step. Stop and ask me where it says so. Answer me in Korean.
```

에이전트가 이 저장소에서 Cladex를 내려받아 설정하고, 에이전트와 휴대폰을 알아서 연결해요. 본인만 이어갈 수 있는 곳에서는 멈추고 물어봐요. Tailscale 로그인, 컴퓨터 주소를 인터넷에 공개하는 일(하기 전에 물어봐요), Hermes와 OpenClaw(본인의 동의가 필요해요), 음성 키(채팅이 아니라 가려진 입력란에 직접 입력해요), Claude 앱의 관리 세션, 그리고 휴대폰의 코드예요. 관리자 권한은 쓰지 않아요.

먼저 [AGENT-INSTALL.md](AGENT-INSTALL.md)를 읽어 보세요. 짧은 문서이고, 에이전트가 정확히 이 내용을 따라가요. 인터넷에 접속할 수 없는 에이전트에게는 주소 대신 파일 자체를 줄 수 있어요.

## 필요한 것

- Apple 칩이 들어간 Mac(M1 이상)과 macOS 15 이상. Linux와 Windows는 창이 없는 미리보기 버전이에요(설치 참고). Intel 칩 Mac용 빌드는 아직 없어요.
- 개인용 무료 Tailscale 계정(tailscale.com/download/mac). 컴퓨터에 인터넷 주소를 만들어 줘요. 휴대폰에는 Tailscale을 설치하지 않아도 돼요.
- 컴퓨터에 로그인된 AI 에이전트가 하나 이상. Claude Code(claude.com/download), Codex(developers.openai.com/codex/app), Hermes(hermes-agent.nousresearch.com/docs/getting-started/installation), OpenClaw(docs.openclaw.ai/install) 중 하나예요. Claude Code에는 유료 claude.ai 요금제가 필요해요.
- Even G2 안경과 휴대폰의 Even 앱.

## 설치

내 컴퓨터를 골라 주세요. 컴퓨터마다 명령과 실행 방법이 달라요.

### Apple 칩 Mac(M1 이상)

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

실행 방법:

1. Cmd+Space를 누르고 터미널(Terminal)을 입력한 다음 Enter를 눌러요. 글자를 입력하는 줄이 있는 창이 열려요.
2. 위의 명령을 복사해서 그 창에 붙여 넣고(Cmd+V) Enter를 눌러요.
3. 무엇을 했는지 알려 줄 때까지 기다려요. 스크립트가 비밀번호를 묻지는 않아요.

그다음에 보이는 것: Cladex 창이 열리고, 첫 설정을 한 단계씩 안내해 줘요(아래 절 참고).

스크립트가 하는 일: 디스크 이미지를 내려받고, 체크섬과 서명, Apple의 공증을 확인해요. 그런 다음 Cladex.app을 응용 프로그램 폴더에 복사하고, 이미지를 닫고, Cladex를 열어요. 확인을 통과하기 전에는 아무것도 바꾸지 않아요. /Applications에 쓸 수 없으면 홈 폴더의 Applications 폴더를 쓰고 그렇다고 알려 줘요. Cladex가 실행 중이면 먼저 종료하라고 안내해요. 옵션: `--no-open`, `--dir <folder>`, `--help`(줄 뒤에 `| sh -s -- --no-open`처럼 붙여요).

직접 설치하는 방법: https://github.com/vsiioky/cladex/releases 를 열어 cladex-arm64.dmg를 내려받고, 열어서 Cladex를 응용 프로그램으로 끌어다 놓은 다음 거기서 열어요. 같은 페이지의 SHA256SUMS로 체크섬을 비교할 수 있어요(`shasum -a 256 cladex-arm64.dmg`).

상태: 릴리스의 서명되고 공증된 디스크 이미지로 실제 Mac에서 확인했어요.

### Intel 칩 Mac

아직 빌드가 없어요. 같은 명령을 실행하면 그렇다는 것을 한 문장으로 알려 주고, 아무것도 바꾸지 않고 멈춰요. 소식은 릴리스 페이지에서 확인해 주세요.

### Linux(x64와 arm64), 미리보기

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

실행 방법:

1. 터미널을 열어요(대부분의 데스크톱에서는 Ctrl+Alt+T, 또는 프로그램 메뉴에서 "터미널"을 찾아요).
2. 위의 명령을 복사해서 붙여 넣고(Ctrl+Shift+V) Enter를 눌러요.
3. 같은 창에 나오는 질문에 답해요. 답하기 전에는 아무것도 바뀌지 않아요.

그다음에 보이는 것: 창은 없어요. 스크립트가 Cladex를 ~/.g2-claude 아래에 두고, `cladex` 명령을 경로에 추가한 다음 `cladex setup`을 시작해요. 질문은 터미널에 나와요. 끝나면 다음 명령을 차례로 실행해요. `cladex gateway init`, `cladex gateway publish`, `cladex pair`예요(`cladex pair`는 컴퓨터 주소와 코드를 보여 줘요). 설치만 하려면 `| sh -s --` 뒤에 `--no-setup`을 붙여요. curl, tar, gzip, xz(패키지 xz-utils)가 필요해요. sudo는 쓰지 않고, Node.js 22를 스스로 내려받아 체크섬을 확인해요.

상태: 미리보기예요. Debian 컨테이너(arm64)에서 설치, `cladex --version`, `cladex setup --print`를 시험했어요. 실제 Linux 컴퓨터, 실제 서비스(systemd), Tailscale, 에이전트로는 시험하지 않았어요.

### Windows 10과 11, 미리보기

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

실행 방법:

1. 시작 메뉴를 열고 PowerShell을 입력한 다음 Enter를 눌러요("관리자 권한으로 실행"이 아닌 일반 창이에요).
2. 위의 명령을 복사해서 붙여 넣고(마우스 오른쪽 클릭으로 붙여 넣어져요) Enter를 눌러요.
3. 같은 창에 나오는 질문에 답해요. 답하기 전에는 아무것도 바뀌지 않아요.

그다음에 보이는 것: Cladex 창은 없어요. 스크립트가 Cladex를 사용자 폴더 아래(.g2-claude)에 두고, 명령 폴더를 사용자 경로에 추가한 다음 `cladex setup`을 시작해요. 질문은 PowerShell에 나와요. 끝나면 `cladex gateway init`, `cladex gateway publish`, `cladex pair`를 차례로 실행해요. 설치만 하려면 줄 앞에 `$env:CLADEX_NO_SETUP = '1'`을 설정해요. 관리자 권한은 쓰지 않아요.

상태: 미리보기예요. 스크립트는 눈으로 읽고 정적 테스트로만 확인했어요. 실제 Windows 컴퓨터에서는 아직 실행해 보지 않았고, 스크립트를 쓴 컴퓨터의 PowerShell도 구문을 분석하지 않았어요.

## 첫 설정

Mac에서는 Cladex 창이 다음 단계를 그때그때 알려 줘요. Linux와 Windows에서는 터미널의 `cladex setup`과 `cladex status`가 알려 줘요. 간단히 정리하면 이래요.

1. Cladex를 열어요. 설치 계획을 읽고 단 하나의 질문에 답해요. 답하기 전에는 아무것도 바뀌지 않아요.
2. Tailscale(tailscale.com/download/mac)을 설치하고 열어서 로그인해요. 컴퓨터 이름에 내 이름이 들어 있으면 이름을 바꿔요.
3. 브라우저에서 Tailscale 페이지를 열어요. MagicDNS와 "Enable HTTPS"를 켜고(console.tailscale.com/admin/dns), 정책에 Funnel을 추가해요(console.tailscale.com/admin/acls).
4. Cladex에서 "주소 공개"를 누르고 컴퓨터 주소를 적어 둬요. name.tailnet.ts.net 같은 모양이고, 인터넷에 나타나기까지 최대 10분이 걸릴 수 있어요.
5. 위 목록에서 AI 에이전트를 설치하고 로그인해요. Cladex는 다른 프로그램을 설치하지 않고, "다시 확인"을 누르면 에이전트를 스스로 찾아요. Claude Code라면 창에 한 번만 하는 관리 세션 단계도 나와요.
6. 음성은 선택이고, ElevenLabs(elevenlabs.io/app/settings/api-keys)나 OpenAI(platform.openai.com/api-keys)의 내 키가 필요해요. Cladex의 설정에 붙여 넣어요.

## 안경용 앱

안경용 Cladex 앱은 Even 베타 채널에 있어요. Even이 카탈로그에 올릴 때까지는 초대로만 받을 수 있고, 초대는 Even 계정의 이메일로 와요. 초대를 요청하려면 이 저장소(https://github.com/vsiioky/cladex/issues)에 "Beta invitation"이라는 제목으로 issue를 열어 주세요. issue는 공개되니 이메일은 적지 마세요. 답글에서 이메일을 비공개로 보내는 방법을 알려 드려요. 초대를 받으면 휴대폰의 Even 앱에서 베타 빌드를 설치해요.

## 휴대폰 연결

1. 컴퓨터의 Cladex에서 "휴대폰 연결"을 눌러요. 컴퓨터 주소와 8자리 코드가 나타나요.
2. 휴대폰의 Even 앱 안에 있는 Cladex 앱에서 주소와 코드를 입력하고, 이어서 컴퓨터에 나온 3자리 숫자를 입력해요.
3. 안경을 써요. "컴퓨터 없음"이라고 나오면 안경 화면을 탭해요. 목록을 다시 확인해요.

## 업데이트

내 컴퓨터용 설치 줄을 다시 실행해요. Mac에서는 실행 중인 Cladex를 먼저 종료해야 하고, 이전 사본은 새 것으로 바뀌어요. Linux와 Windows에서는 `cladex update` 가 같은 일을 스스로 해요. 최신 릴리스를 내려받고, 체크섬을 확인하고, 실행 중인 사본 옆에 두고 서비스를 다시 시작해요. 새 버전이 응답하지 않으면 서비스가 스스로 이전 버전으로 되돌아가요. 설정과 휴대폰은 그대로 남아요.

Cladex는 하루에 한 번 GitHub에 더 새로운 릴리스가 있는지 물어보고(GitHub에는 인터넷상의 내 주소와 Cladex 버전만 보여요), 있으면 `cladex status` 가 알려 줘요. `cladex update check off` 로 이 확인을 끄고, `cladex update check on` 으로 다시 켤 수 있어요. 확인이 꺼져 있는 동안에는 보안 문제와 오류의 수정이 도착하지 않고, 새 버전이 나와도 아무것도 알려 주지 않으며, Even 을 통해 스스로 업데이트되는 안경 앱이 컴퓨터의 오래된 버전을 더 이상 이해하지 못할 수 있어요. Cladex는 `cladex update auto on` 으로 허용했을 때만 새 버전을 스스로 설치해요. `cladex update auto off` 로 다시 금지할 수 있어요. `cladex update status` 로 이 모든 것을 볼 수 있어요.

## 제거

Cladex에서 설정을 열고 "제거" 그룹의 "이 컴퓨터에서 Cladex 제거..."를 눌러요. 또는 터미널에서 `cladex uninstall`을 실행해요. Cladex가 설치한 모든 것(서비스, 훅, 설정, 키, 로그)이 제거돼요. 그다음 Cladex.app을 휴지통으로 옮겨요. Tailscale과 AI 에이전트는 그대로 남아요.

## 개인정보

- Cladex 서버도 계정도 없어요. 개발자는 앱이나 프로그램에서 어떤 데이터도 받지 않아요.
- 분석도, 광고도, 추적도 없어요.
- 내 음성은 내 컴퓨터로만 가고, 거기서 내 키로 음성 인식 서비스에 가요.

전문: [PRIVACY.md](PRIVACY.md)(영어). 이용 약관: [TERMS.md](TERMS.md)(영어).

## 소개

Cladex의 소스 코드는 공개하지 않아요. Cladex는 독립적인 프로젝트이며 Anthropic, OpenAI, Nous Research, OpenClaw, Even Realities, Tailscale과 제휴 관계가 없고 이들의 보증을 받지 않았어요. 제품 이름은 각 소유자에게 있어요. 질문과 문제는 이 저장소의 Issues로 보내 주세요.

## Cladex 후원하기

Cladex는 무료이고 앞으로도 무료예요. 도움이 되었다면 개발을 후원할 수 있어요: ko-fi.com/cladex.
