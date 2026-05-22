---
name: codex-image
description: "通过 Codex CLI (ChatGPT Plus) 免费生图。需安装 Codex 并登录 ChatGPT Plus。特点：文字渲染精准、照片级真实度。"
allowed-tools: Bash(python3 *)
---

# Codex Image（Codex 通道）

通过 Codex CLI + ChatGPT Plus 订阅免费生图，**不走 API 计费**。

> 前提：已安装 Codex 并登录 ChatGPT Plus
> 注意：使用此工具会消耗您的 ChatGPT Plus 账号每 3 小时的消息对话额度（适用于 DALL-E 3 和 GPT-4）。

## 使用方式

```bash
python3 ~/.claude/skills/codex-image/generate.py "<提示词>" [尺寸] [输出目录]
```

| 参数 | 说明 | 默认值 |
|------|------|--------|
| prompt | 生图提示词 | 必填 |
| size | 尺寸 | `1024x1024` |
| output_dir | 保存目录 | 当前目录 |

## 示例

```bash
# 方形
python3 ~/.claude/skills/codex-image/generate.py "一只橘猫睡在沙发上，阳光洒落"

# 横版
python3 ~/.claude/skills/codex-image/generate.py "未来城市天际线，黄昏时分" 1536x1024

# 竖版 + 指定目录
python3 ~/.claude/skills/codex-image/generate.py "日式枯山水庭院" 1024x1536 ~/Desktop
```

## 原理

Codex CLI 走 ChatGPT 订阅通道，生图没有额外的 API 费用，但会消耗 Plus 包含的消息额度。
