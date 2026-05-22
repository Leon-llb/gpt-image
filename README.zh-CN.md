<p align="center">
  <picture>
    <img alt="Codex Image" src="https://raw.githubusercontent.com/Leon-llb/codex-image/main/assets/logo.svg" width="120">
  </picture>
</p>

<h1 align="center">Codex Image</h1>

<p align="center">
  <sub>🌐 <a href="README.md">English</a></sub>
</p>

<p align="center">
  用你的 ChatGPT Plus 订阅实现 AI 生图。<br>
  零 API 费用。零 Token 消耗。只有你的 Plus 订阅和 Codex CLI。
</p>

<p align="center">
  <a href="https://github.com/Leon-llb/codex-image/releases"><img src="https://img.shields.io/github/v/release/Leon-llb/codex-image?color=blue&label=version" alt="Version"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-green" alt="License MIT"></a>
  <a href="#"><img src="https://img.shields.io/badge/platform-macOS%20%7C%20Windows-silver" alt="Platform macOS | Windows"></a>
  <a href="https://codex.chat"><img src="https://img.shields.io/badge/requires-ChatGPT%20Plus%20%7C%20Codex-orange" alt="Requires ChatGPT Plus | Codex"></a>
  <a href="#"><img src="https://img.shields.io/github/stars/Leon-llb/codex-image?style=social" alt="Stars"></a>
</p>

---

## 这是什么

Codex Image 让任何 CLI 工具或 AI Agent 都能生图——通过 [Codex 客户端](https://codex.chat) 走你已有的 ChatGPT Plus 订阅通道。

- 无需 API Key
- 无 Token 计费
- 无第三方中转
- 就是 Codex 客户端 + 你的 Plus 订阅

## 为什么用这个

| | Codex Image | API 方案 |
|---|---|---|
| 费用 | 不走 API 计费（消耗 Plus 额度） | 按张计费 |
| 模型 | ChatGPT 原生图像模型 | 看 API |
| 文字渲染 | 精准 | 参差不齐 |
| 上手 | 一行 `git clone` | 注册、绑卡、充值 |
| 依赖 | Codex（有 Plus 就已装好） | 无 |

## 前置条件

| 条件 | 说明 |
|---|---|
| 操作系统 | macOS 或 Windows |
| [Codex](https://codex.chat) | 桌面客户端，提供 `codex` 命令 |
| ChatGPT Plus | 生图走 Plus 额度（适用于 DALL-E 3 消息配额） |

> 没有 Plus？去 [chatgpt.com/upgrade](https://chatgpt.com/upgrade) 升级

## 快速开始

```bash
# 1. 克隆
git clone https://github.com/Leon-llb/codex-image.git ~/.claude/skills/codex-image

# 2. 生图
python3 ~/.claude/skills/codex-image/generate.py "一只橘猫睡在沙发上，阳光洒落"
```

## 用法

```
python3 generate.py "<prompt>" [size] [output_dir]
```

| 参数 | 默认值 | 说明 |
|---|---|---|
| `prompt` | 必填 | 生图提示词 |
| `size` | `1024x1024` | 尺寸，`宽x高` 格式 |
| `output_dir` | 当前目录 | 图片保存位置 |

```bash
# 正方形
python3 generate.py "一只柴犬，日系插画风，纯白背景"

# 竖版海报
python3 generate.py "电影感肖像，黄金时刻光线，8k" 1024x1536 ~/Downloads

# 横版壁纸
python3 generate.py "赛博朋克城市夜景，霓虹灯光" 1536x1024 ~/Desktop
```

图片自动命名为 `codex-image-20260518-143052.png`。

## 集成方式

### Claude Code

放到 skills 目录，Claude Code 自动发现：

```bash
ln -sf ~/.claude/skills/codex-image ~/.claude/skills/codex-image
```

对话里说「生成一张 xxx 的图」即可触发。

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

之后在 Telegram/微信跟 Agent 说「帮我生成一张 xxx 的图」，Agent 的 `image_generate` 工具自动路由到 codex-image provider，执行 `generate.py`，图片保存到 `~/Downloads`。

## 原理

```
用户 → Hermes/Claude → image_generate 工具调用
                           ↓
                  codex-image provider
                           ↓
                    generate.py 脚本
                           ↓
                 codex exec (ChatGPT Plus)
                           ↓
                    图片 → ~/Downloads
```

不走 OpenAI API，不产生额外费用。只是把你 Plus 订阅已有的能力释放出来（注意：此操作会消耗你的 ChatGPT Plus 中 DALL-E 3 的对话限额）。

## License

MIT — [Leon](https://github.com/Leon-llb)
