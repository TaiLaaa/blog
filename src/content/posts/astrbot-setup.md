---
title: 用 AstrBot 打造 QQ 群聊 AI 助手
published: 2026-03-18
description: "从零部署 AstrBot，配置多 LLM 服务商，打造能聊天、发表情、跨群感知的智能群助手。"
tags: ["AstrBot", "QQ机器人", "AI", "Docker"]
category: "技术"
draft: false
---

## 为什么选 AstrBot？

市面上 QQ 机器人框架不少，但 AstrBot 有几个让我很满意的点：

- **多 LLM 支持**：同时接入 DeepSeek、Gemini、GPT、Kimi 等多个模型
- **插件生态**：Python 写插件门槛低，API 设计清晰
- **Docker 部署**：一行命令跑起来

## 快速部署

```bash
docker run -d --name astrbot \
  --restart always \
  -e TZ=Asia/Shanghai \
  -p 6185:6185 \
  -v /root/astrbot/data:/AstrBot/data \
  soulter/astrbot:latest
```

Dashboard 打开 `http://你的IP:6185` 就能用。

## 我写的几个插件

### 跨会话感知 (cross_session_awareness)

让 bot 记住用户在不同群/私聊的发言，实现跨群上下文关联：

> 用户在 A 群：「我今天买了只布偶猫」
> 用户在 B 群 @bot：「你好」
> bot：「嗨～听说你入手了布偶猫？叫什么名字？」

技术要点：
- `event_message_type(ALL)` 全量消息监听
- LLM 异步生成摘要存储
- 支持图片识别（Vision 模型）

### 内容审核 (content_guardian)

LLM + 关键词双引擎，递进式处罚：

1. 第1次：撤回 + 警告
2. 第2次：撤回 + 禁言
3. 第3次：撤回 + 踢出

关键词命中零 LLM 消耗，审核+警告合并为一次调用，省钱。

## 小结

折腾了一天，效果超预期。AstrBot 的插件 API 设计得不错，写起来很顺手。
