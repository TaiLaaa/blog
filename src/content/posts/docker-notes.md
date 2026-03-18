---
title: Docker 容器网络踩坑记录
published: 2026-03-15
description: "Docker 自定义网络、端口映射和容器间通信的一些坑。"
tags: ["Docker", "网络", "运维"]
category: "技术"
draft: false
---

## 端口映射不生效？

部署 AstrBot 时遇到经典问题：容器内 5000 端口的服务外面访问不到。

原因——创建容器时只映射了主服务端口：

```bash
# ❌ 只映射了 6185
docker run -p 6185:6185 ...

# ✅ 把需要的端口都映射上
docker run -p 6185:6185 -p 5000:5000 ...
```

Docker **不支持**给已运行的容器追加端口映射，只能重建。数据卷挂载了宿主机目录，重建不丢数据。

## 容器间通信

同一个 `docker network` 里的容器可以用容器名互相访问：

```bash
# 容器 A 访问容器 B
curl http://container-b:8080
```

## 教训

- 部署前想清楚所有需要暴露的端口
- 数据一定要挂载到宿主机
- `docker logs --since 30s <container>` 是你最好的朋友
