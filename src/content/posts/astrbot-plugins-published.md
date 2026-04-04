---
title: 两个 AstrBot 插件提交了插件市场
published: 2026-04-04
description: "跨会话感知和哔哩哔哩视频解析两个插件已提交到 AstrBot 官方插件市场，等待审核收录。"
tags: ["AstrBot", "QQ机器人", "插件开发", "AI"]
category: "技术"
draft: false
---

今天把两个插件提交到了 AstrBot 官方插件市场，记录一下。

## 提交了什么

### 跨会话感知

让 bot 拥有跨群记忆能力，记住各群和私聊里发生的事情。

核心功能：

- 用户跨会话记忆：在 A 群说的话，bot 在 B 群认识你时会记得
- 群聊上下文感知：记录各群对话流，生成摘要，bot 能在其他群被问起时引用
- 合并转发感知：读取群友分享的聊天记录，结合后续讨论一起摘要

仓库：[astrbot_plugin_cross_session_awareness](https://github.com/TaiLaaa/astrbot_plugin_cross_session_awareness)

### 哔哩哔哩视频解析

识别消息中的 B 站链接，自动生成 AI 总结。

核心功能：

- 支持 @bot + 视频链接、私聊直接发链接、回复带链接的消息等触发方式
- 关键帧理解：下载视频后抽帧，让模型直接「看视频」
- T2I 输出：用 Playwright 渲染成图片发出
- 自动安装依赖，开启 T2I 后会自动补齐 yt-dlp、playwright、Chromium

仓库：[astrbot_plugin_video_summary](https://github.com/TaiLaaa/astrbot_plugin_video_summary)

## 提交流程

AstrBot 插件市场的提交方式是在 GitHub 上创建 Issue，按固定 JSON 格式填写插件信息，维护者审核后手动收录进 plugins.json。

两个 Issue 链接：
- [#489 跨会话感知](https://github.com/AstrBotDevs/AstrBot_Plugins_Collection/issues/489)
- [#490 哔哩哔哩视频解析](https://github.com/AstrBotDevs/AstrBot_Plugins_Collection/issues/490)

等审核结果。
