---
name: codex-image
description: "Free AI image generation via Codex CLI (ChatGPT Plus). Requires Codex.app installed and logged into a ChatGPT Plus account. Features: accurate text rendering, photorealistic quality."
allowed-tools: Bash(python3 *)
---

# Codex Image (via Codex CLI)

Free image generation through Codex CLI + ChatGPT Plus subscription. **No API billing.**

> Prerequisite: Codex.app installed and logged into ChatGPT Plus

## Usage

```bash
python3 ~/.claude/skills/codex-image/generate.py "<prompt>" [size] [output_dir]
```

| Argument | Description | Default |
|----------|-------------|---------|
| prompt | Image generation prompt | required |
| size | Dimensions | `1024x1024` |
| output_dir | Save location | current directory |

## Examples

```bash
# Square
python3 ~/.claude/skills/codex-image/generate.py "a orange cat sleeping on a sofa, sunlight streaming in"

# Landscape
python3 ~/.claude/skills/codex-image/generate.py "a futuristic city skyline at dusk" 1536x1024

# Portrait with output dir
python3 ~/.claude/skills/codex-image/generate.py "a japanese zen garden" 1024x1536 ~/Desktop
```

## How it works

Codex CLI routes through your ChatGPT subscription — image generation costs nothing extra (included in Plus).
