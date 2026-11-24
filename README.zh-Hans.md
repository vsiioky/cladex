# Cladex

[English](README.md) | [Русский](README.ru.md) | [Deutsch](README.de.md) | [Français](README.fr.md) | [Español](README.es.md) | [Italiano](README.it.md) | **简体中文** | [繁體中文](README.zh-Hant.md) | [日本語](README.ja.md) | [한국어](README.ko.md)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/cladex)

Cladex 是一个遥控器，用 Even G2 眼镜查看并控制在你自己的电脑上工作的 AI 智能体。

- 你在每台运行 AI 智能体的电脑上安装一个程序。它是带有自己窗口的 Mac 应用。
- 眼镜（通过手机上的 Even 应用）会显示你的智能体、它们的会话和提问，你可以用触摸或语音来回答。
- 一切都从手机直接发到你自己的电脑，使用各台电脑自己的地址。没有 Cladex 服务器，也没有 Cladex 账号。
- 支持 Claude Code、Codex、Hermes 和 OpenClaw。
- 这个仓库只有安装包和说明。源代码不公开。

## 让你的 AI 智能体来安装

如果你在这台电脑上使用的 AI 智能体可以使用终端（Claude Code、Codex、Hermes、OpenClaw 或其他），可以让它来完成安装。把下面这段话复制给智能体：

```
Install Cladex on this computer. Read https://raw.githubusercontent.com/vsiioky/cladex/main/AGENT-INSTALL.md and follow it step by step. Stop and ask me where it says so. Answer me in Simplified Chinese.
```

智能体会从这个仓库下载 Cladex，完成设置，并自行把你的智能体和手机连起来。遇到只有你才能继续的地方，它会停下来询问：登录 Tailscale、把电脑的地址开放到互联网（操作之前会先问你）、Hermes 和 OpenClaw（需要你同意）、语音密钥（你在隐藏输入的提示里自己输入，绝不会写进聊天）、Claude 应用里的调度器，以及手机上的配对码。它从不使用管理员权限。

请先阅读 [AGENT-INSTALL.md](AGENT-INSTALL.md)：它很短，智能体正是照着它来做。对于无法访问互联网的智能体，可以直接把这个文件交给它，而不是给它地址。

## 你需要准备什么

- 搭载 Apple 芯片（M1 或更新）的 Mac，系统为 macOS 15 或更新。Linux 和 Windows 是没有窗口的预览版（见“安装”）；搭载 Intel 芯片的 Mac 目前还没有安装包。
- 一个个人使用的免费 Tailscale 账号（tailscale.com/download/mac）。它为电脑提供互联网上的地址。手机上不需要安装 Tailscale。
- 电脑上至少有一个已登录的 AI 智能体：Claude Code（claude.com/download）、Codex（developers.openai.com/codex/app）、Hermes（hermes-agent.nousresearch.com/docs/getting-started/installation）或 OpenClaw（docs.openclaw.ai/install）。Claude Code 需要付费的 claude.ai 套餐。
- Even G2 眼镜，以及手机上的 Even 应用。

## 安装

请选择你的电脑。每种电脑有各自的命令和运行方式。

### 搭载 Apple 芯片的 Mac（M1 或更新）

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

运行方法：

1. 按 Cmd+空格，输入“终端”（Terminal），然后按回车。会打开一个带文字输入行的窗口。
2. 复制上面的命令，粘贴到这个窗口里（Cmd+V），然后按回车。
3. 等它说明做了什么。这个脚本从不索要你的密码。

接下来你会看到：Cladex 的窗口会打开，一步一步带你完成首次设置（见下面一节）。

脚本做了什么：下载磁盘映像，检查它的校验和、签名以及 Apple 的公证，把 Cladex.app 复制到“应用程序”，关闭映像，然后打开 Cladex。检查全部通过之前，它不会改动任何东西。如果 /Applications 不可写，它会改用你主目录里的 Applications 文件夹，并告诉你。如果 Cladex 正在运行，它会请你先退出。选项：`--no-open`、`--dir <folder>`、`--help`（写在命令行后面：`| sh -s -- --no-open`）。

手动安装：打开 https://github.com/vsiioky/cladex/releases，下载 cladex-arm64.dmg，打开它，把 Cladex 拖到“应用程序”，然后从那里打开。同一页面上的 SHA256SUMS 可用来核对校验和（`shasum -a 256 cladex-arm64.dmg`）。

状态：已在真实的 Mac 上用该版本已签名并经过公证的磁盘映像验证。

### 搭载 Intel 芯片的 Mac

目前还没有安装包。运行同一条命令，它会用一句话说明这一点，并且不做任何改动就停止。请留意发布页面上的消息。

### Linux（x64 和 arm64），预览版

```sh
curl -fsSL https://github.com/vsiioky/cladex/releases/latest/download/install.sh | sh
```

运行方法：

1. 打开终端（大多数桌面环境中按 Ctrl+Alt+T，或在程序菜单里找“终端”）。
2. 复制上面的命令，粘贴（Ctrl+Shift+V），然后按回车。
3. 回答同一窗口里出现的问题。你回答之前不会有任何改动。

接下来你会看到：没有窗口。脚本把 Cladex 放在 ~/.g2-claude 下，把 `cladex` 命令加入你的路径，并启动 `cladex setup`，它会在终端里提问。结束后，依次运行这些命令：`cladex gateway init`，然后 `cladex gateway publish`，再 `cladex pair`（它会打印电脑的地址和一个配对码）。如果只想安装，在 `| sh -s --` 后面加上 `--no-setup`。它需要 curl、tar、gzip 和 xz（软件包 xz-utils），从不使用 sudo，并会自己下载 Node.js 22 并检查其校验和。

状态：预览版。已在 Debian 容器（arm64）里测试：安装、`cladex --version` 和 `cladex setup --print`。尚未在真实的 Linux 电脑、真实的服务（systemd）、Tailscale 或智能体上测试。

### Windows 10 和 11，预览版

```powershell
irm https://github.com/vsiioky/cladex/releases/latest/download/install.ps1 | iex
```

运行方法：

1. 打开“开始”菜单，输入 PowerShell，然后按回车（是普通窗口，不要选“以管理员身份运行”）。
2. 复制上面的命令，粘贴（点鼠标右键即可粘贴），然后按回车。
3. 回答同一窗口里出现的问题。你回答之前不会有任何改动。

接下来你会看到：不会出现 Cladex 的窗口。脚本把 Cladex 放在你的用户文件夹下（.g2-claude），把它的命令文件夹加入你用户的路径，并启动 `cladex setup`，它会在 PowerShell 里提问。结束后运行：`cladex gateway init`，然后 `cladex gateway publish`，再 `cladex pair`。如果只想安装，在运行那一行之前先设置 `$env:CLADEX_NO_SETUP = '1'`。不使用管理员权限。

状态：预览版。脚本只经过人工阅读和静态测试：还没有在真实的 Windows 电脑上运行过，而且在编写它的那台机器上，PowerShell 也没有解析过它。

## 首次设置

在 Mac 上，Cladex 的窗口会指出每一步；在 Linux 和 Windows 上，由终端里的 `cladex setup` 和 `cladex status` 指出。简要如下：

1. 打开 Cladex。阅读安装计划，回答它的那一个问题。你回答之前不会有任何改动。
2. 安装 Tailscale（tailscale.com/download/mac），打开并登录。如果电脑的名称里有你自己的名字，请给电脑改名。
3. 在浏览器里打开 Tailscale 的页面：打开 MagicDNS 和“Enable HTTPS”（console.tailscale.com/admin/dns），并把 Funnel 加入策略（console.tailscale.com/admin/acls）。
4. 在 Cladex 里点“发布地址”，并记下电脑的地址。它的形式类似 name.tailnet.ts.net，最多可能需要 10 分钟才会出现在互联网上。
5. 安装上面列表中的一个 AI 智能体并登录。Cladex 不会安装其他程序，点“重新检查”后会自己找到智能体。对于 Claude Code，窗口里还会出现一次性的调度器步骤。
6. 语音是可选的，需要你自己的 ElevenLabs（elevenlabs.io/app/settings/api-keys）或 OpenAI（platform.openai.com/api-keys）密钥。把它粘贴到 Cladex 的设置里。

## 眼镜应用

眼镜上的 Cladex 应用在 Even 的测试版渠道中。在 Even 把它列入应用目录之前，需要受邀才能使用，邀请会发到你 Even 账号的邮箱。要申请邀请，请在这个仓库（https://github.com/vsiioky/cladex/issues）里创建一个 issue，标题写“Beta invitation”。请不要在 issue 里写你的邮箱：issue 是公开的，回复中会说明如何私下发送邮箱。收到邀请后，在手机上的 Even 应用里安装测试版。

## 配对手机

1. 在电脑上的 Cladex 里点“配对手机”：会出现电脑的地址和一个 8 位配对码。
2. 在手机上 Even 应用里的 Cladex 应用中输入地址和配对码，然后输入电脑上显示的 3 位数字。
3. 戴上眼镜。如果显示“没有电脑”，点一下眼镜的屏幕：列表会重新检查。

## 更新

再次运行你那台电脑的安装命令：在 Mac 上必须先退出正在运行的 Cladex，旧版本会被替换。在 Linux 和 Windows 上，`cladex update` 会自己完成同样的事：下载最新发布，核对校验和，放到正在运行的副本旁边并重启服务；如果新版本没有响应，服务会自己退回上一个版本。你的设置和你的手机都会保留。

Cladex 每天向 GitHub 询问一次是否有更新的发布（GitHub 只能看到你在互联网上的地址和 Cladex 的版本，别的都看不到），有的话 `cladex status` 会告诉你。`cladex update check off` 关闭这项检查，`cladex update check on` 重新打开。检查关闭期间，安全问题和错误的修复不会送达，也不会有任何东西告诉你有新版本，而眼镜上通过 Even 自动更新的应用，可能无法再识别电脑上的旧版本。只有你用 `cladex update auto on` 允许之后，Cladex 才会自己安装新版本；`cladex update auto off` 可以再次禁止。`cladex update status` 会显示以上全部。

## 移除

在 Cladex 里打开设置，找到“移除”组，点“从这台电脑移除 Cladex...”。或者在终端里运行 `cladex uninstall`：它会移除 Cladex 安装的所有内容（服务、hooks、设置、密钥、日志）。然后把 Cladex.app 移到废纸篓。Tailscale 和你的 AI 智能体都会保留。

## 隐私

- 没有 Cladex 服务器，也没有账号。开发者不会从应用或程序收到任何数据。
- 没有统计分析，没有广告，没有跟踪。
- 你的语音只发到你自己的电脑，再由电脑用你自己的密钥发给语音服务。

全文：[PRIVACY.md](PRIVACY.md)（英文）。使用条款：[TERMS.md](TERMS.md)（英文）。

## 关于

Cladex 的源代码不公开。Cladex 是独立项目，与 Anthropic、OpenAI、Nous Research、OpenClaw、Even Realities 或 Tailscale 没有关联，也未获得它们的认可。产品名称归其各自所有者所有。问题和反馈：请到这个仓库的 Issues。

## 支持 Cladex

Cladex 是免费的，并将一直免费。如果它对你有帮助，你可以支持它的开发：ko-fi.com/cladex。
