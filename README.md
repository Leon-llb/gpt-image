<p align="center">
  <picture>
    <img alt="Codex Image" src="https://raw.githubusercontent.com/Leon-llb/codex-image/main/assets/logo.svg" width="120">
  </picture>
</p>

<h1 align="center">Codex Image</h1>

<p align="center">
  Free AI image generation powered by your ChatGPT Plus subscription.<br>
  Zero API cost. Zero tokens. Just your Plus sub and Codex CLI.
</p>

<p align="center">
  <a href="https://github.com/Leon-llb/codex-image/releases"><img src="https://img.shields.io/github/v/release/Leon-llb/codex-image?color=blue&label=version" alt="Version"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-green" alt="License MIT"></a>
  <a href="#"><img src="https://img.shields.io/badge/platform-macOS-silver" alt="Platform macOS"></a>
  <a href="https://codex.chat"><img src="https://img.shields.io/badge/requires-ChatGPT%20Plus%20%7C%20Codex.app-orange" alt="Requires ChatGPT Plus | Codex.app"></a>
  <a href="#"><img src="https://img.shields.io/github/stars/Leon-llb/codex-image?style=social" alt="Stars"></a>
</p>

---

## What is this

Codex Image lets any CLI tool or AI agent generate images for free — by routing through your ChatGPT Plus subscription via [Codex CLI](https://codex.chat).

- No API key
- No token billing
- No third-party proxy
- Just Codex CLI + your Plus subscription

## Why Codex Image

| | Codex Image | API-based |
|---|---|---|
| Cost | Free (included in Plus) | Pay per image |
| Model | ChatGPT native image model | Varies by API |
| Text rendering | Accurate | Hit or miss |
| Setup | One `git clone` | Register, add card, top up |
| Dependency | Codex.app (already installed if you have Plus) | None |

## Prerequisites

| Requirement | Notes |
|---|---|
| macOS | Codex.app is macOS-only |
| [Codex.app](https://codex.chat) | Desktop client, provides the `codex` CLI |
| ChatGPT Plus | Image generation uses your Plus quota |

> Don't have Plus? Upgrade at [chatgpt.com/upgrade](https://chatgpt.com/upgrade)

## Quick start

```bash
# 1. Clone
git clone https://github.com/Leon-llb/codex-image.git ~/.claude/skills/codex-image

# 2. Generate
python3 ~/.claude/skills/codex-image/generate.py "a cat sleeping on a sofa, warm sunlight"
```

## Usage

```
python3 generate.py "<prompt>" [size] [output_dir]
```

| Argument | Default | Description |
|---|---|---|
| `prompt` | required | Image generation prompt |
| `size` | `1024x1024` | Dimensions as `WxH` |
| `output_dir` | cwd | Where to save the image |

```bash
# Square
python3 generate.py "a shiba inu, japanese illustration style, white background"

# Portrait poster
python3 generate.py "a cinematic portrait, golden hour lighting, 8k" 1024x1536 ~/Downloads

# Landscape wallpaper
python3 generate.py "cyberpunk city skyline at night, neon lights" 1536x1024 ~/Desktop
```

Images are saved with the filename pattern `codex-image-20260518-143052.png`.

## Integrations

### Claude Code

Drop the skill into your skills directory and Claude Code discovers it automatically:

```bash
ln -sf ~/.claude/skills/codex-image ~/.claude/skills/codex-image
```

Say "generate an image of..." in conversation to trigger it.

### Hermes / OpenClaw Agent

Let your Telegram or WeChat agent generate images too.

**Install the plugin**

```bash
mkdir -p ~/.hermes/hermes-agent/plugins/image_gen/codex-image
cp hermes-plugin/plugin.yaml ~/.hermes/hermes-agent/plugins/image_gen/codex-image/
cp hermes-plugin/__init__.py ~/.hermes/hermes-agent/plugins/image_gen/codex-image/
```

**Configure `~/.hermes/config.yaml`**

```yaml
plugins:
  enabled:
    - image_gen/codex-image

image_gen:
  provider: codex-image
```

**Restart**

```bash
hermes gateway restart
```

Now when someone messages your Hermes agent "generate an image of X", the agent's built-in `image_generate` tool routes to the codex-image provider, which runs `generate.py`, and the image lands in `~/Downloads`.

## How it works

```
User → Hermes/Claude → image_generate tool call
                           ↓
                  codex-image provider
                           ↓
                    generate.py script
                           ↓
                 codex exec (ChatGPT Plus)
                           ↓
                    Image → ~/Downloads
```

No OpenAI API calls. No extra billing. Just your Plus subscription doing what it already pays for.

## License

MIT — [Leon](https://github.com/Leon-llb)
