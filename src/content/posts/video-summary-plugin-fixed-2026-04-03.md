---
title: 视频解析插件修好了
published: 2026-04-03
description: "AstrBot 哔哩哔哩视频解析插件的人格继承和追问误触发问题，目前已全部修复。"
tags: ["AstrBot", "插件开发", "AI", "视频解析", "问题修复"]
category: "技术"
draft: false
---

上次写了一篇翻车记录，把当时的问题都记下来了。这次简短更新一下：**两个问题都修好了**。

## 修了什么

### 1. 人格继承问题

视频解析插件在走自己的 LLM 调用链路时，没有正确拿到当前对话绑定的人格。

现在改成了多级兜底读取：

1. session_service_config.persona_id
2. 当前对话的 conversation.persona_id
3. UMO 默认人格
4. selected_default_persona fallback

按顺序往下找，和 AstrBot 主聊天链路保持一致。视频解析开场白、总结正文、追问回复，现在都会按当前人格走了。

### 2. 追问误触发

原来只要"回复了 Bot 且存在视频上下文"就可能进 follow-up，导致吐槽句、打断句也被错当成视频追问处理。

现在加了：

- **冷却时间**：视频总结刚发完，不会立刻把下一条都当 follow-up
- **噪音筛选**：短吐槽、情绪句、疑问反问，不再走视频链路
- **上下文完成判断**：必须确实有可用的视频总结结果，才允许 follow-up 接入

## 目前状态

测试区验证稳定，已经推到正式版。

插件现在仅支持哔哩哔哩视频解析（`bilibili.com` / `b23.tv`），人格跟随当前对话设置。

---

GitHub：<https://github.com/TaiLaaa/astrbot_plugin_video_summary>
