<p align="center">
  <picture>
    <img alt="Codex Image" src="https://raw.githubusercontent.com/Leon-llb/codex-image/main/assets/logo.svg" width="120">
  </picture>
</p>

<h1 align="center">Codex Image</h1>

<p align="center">
  通过 ChatGPT Plus 订阅免费生图，不花一分 API 余额。
</p>

<p align="center">
  <a href="https://github.com/Leon-llb/codex-image/releases"><img src="https://img.shields.io/github/v/release/Leon-llb/codex-image?color=blue&label=version" alt="Version"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-green" alt="License MIT"></a>
  <a href="#"><img src="https://img.shields.io/badge/platform-macOS-silver" alt="Platform macOS"></a>
  <a href="https://codex.chat"><img src="https://img.shields.io/badge/requires-ChatGPT%20Plus%20%7C%20Codex.app-orange" alt="Requires ChatGPT Plus | Codex.app"></a>
  <a href="#"><img src="https://img.shields.io/github/stars/Leon-llb/codex-image?style=social" alt="Stars"></a>
</p>

---

## 这是什么

Codex Image 是一个极简的 AI 图片生成工具。它调用你本机已安装的 [Codex.app](https://codex.chat) 来驱动 ChatGPT 的生图能力，**走 Plus 订阅额度，完全免费**。

- 没有 API key
- 没有 token 计费
- 没有第三方中转
- 就是 Codex CLI + 你的 Plus 订阅

## 为什么用这个

| | Codex Image | API 生图 |
|---|---|---|
| 费用 | 免费（Plus 已包含） | 按张计费 |
| 模型 | ChatGPT 原生图像模型 | 取决于 API |
| 文字渲染 | 精准 | 看模型 |
| 安装 | 一行 git clone | 注册、绑卡、充值 |
| 依赖 | Codex.app（已有 Plus 的话已装好） | 无 |

## 前置条件

| 条件 | 说明 |
|---|---|
| macOS | Codex.app 仅支持 macOS |
| [Codex.app](https://codex.chat) | 桌面客户端，提供 `codex` 命令 |
| ChatGPT Plus | 生图走 Plus 额度 |

> 没有 Plus？请先升级：[chatgpt.com/upgrade](https://chatgpt.com/upgrade)

## 快速开始

```bash
# 1. 克隆
git clone https://github.com/Leon-llb/codex-image.git ~/.claude/skills/codex-image

# 2. 生图
python3 ~/.claude/skills/codex-image/generate.py "a cat sleeping on a sofa, warm sunlight"
```

## 用法

```
python3 generate.py "<prompt>" [size] [output_dir]
```

| 参数 | 默认值 | 说明 |
|---|---|---|
| `prompt` | 必填 | 生图提示词 |
| `size` | `1024x1024` | 尺寸，格式 `宽x高` |
| `output_dir` | 当前目录 | 图片保存位置 |

```bash
# 正方形头像
python3 generate.py "一只柴犬，日系插画风，纯白背景" 1024x1024 ~/Downloads

# 竖版海报
python3 generate.py "a cinematic portrait, golden hour lighting, 8k" 1024x1536 ~/Downloads

# 横版壁纸
python3 generate.py "cyberpunk city skyline at night, neon lights" 1536x1024 ~/Desktop
```

图片自动保存到 `~/Downloads`，文件名格式：`codex-image-20260518-143052.png`

## 集成

### Claude Code

放在 skills 目录即可，Claude Code 自动识别：

```bash
ln -sf ~/.claude/skills/codex-image ~/.claude/skills/codex-image
```

对话中说「帮我生成一张 xxx 的图」即可触发。

### Hermes / OpenClaw Agent

让 Telegram、微信消息也能生图。

**安装插件**

```bash
mkdir -p ~/.hermes/hermes-agent/plugins/image_gen/codex-image
cp hermes-plugin/plugin.yaml ~/.hermes/hermes-agent/plugins/image_gen/codex-image/
cp hermes-plugin/__init__.py ~/.hermes/hermes-agent/plugins/image_gen/codex-image/
```

**配置 `~/.hermes/config.yaml`**

```yaml
plugins:
  enabled:
    - image_gen/codex-image

image_gen:
  provider: codex-image
```

**重启**

```bash
hermes gateway restart
```

## 原理

```
用户 → Hermes/Claude → image_generate 工具调用
                           ↓
                    codex-image provider
                           ↓
                    generate.py 脚本
                           ↓
                 codex exec (ChatGPT Plus 订阅)
                           ↓
                    图片 → ~/Downloads
```

全程不走 OpenAI API，不产生额外费用。

## License

MIT — [Leon](https://github.com/Leon-llb)
