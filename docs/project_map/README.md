# project_map — ocr-service 项目地图

本目录按**运行事实**说明本仓库，不是概念词典。

| 文档 | 维度 |
|---|---|
| [positioning.md](positioning.md) | 项目定位：只收图片字节 |
| [architecture.md](architecture.md) | HTTP、引擎、缓存 |
| [tech-stack.md](tech-stack.md) | Python / Paddle / Docker |
| [deployment.md](deployment.md) | 回环 :9188、Compose、**不走 :4220** |
| [release.md](release.md) | 无 `build.sh`；镜像构建即发布 |
| [development.md](development.md) | 单测不需要 Paddle |

根目录 [`AGENT.md`](../../AGENT.md) 是后续 agent 的入口。API 形状以 [`README.md`](../../README.md) 为准。

## 本轮已核对的异议（2026-10-12）

1. **不在部署平台 `:4220` 登记。** 禁止对本服务发 `deploy-notify`。
2. **只绑 `127.0.0.1:9188`。** 不要 publish 到 LAN。
3. **不知道 Asset / Brain / Planner。** `image.ocr` 包装在 Brain。
4. **源码权威是本仓，不是 os。** 云上目录 `/root/chat-gateway/ocr-service` 从此仓 clone。
5. **Dockerfile 基础镜像走 DaoCloud**（`docker.m.daocloud.io/library/python:3.10-bookworm`），不要改回直连 docker.io。
6. **COPY 只有 `engine.py` `cache.py` `main.py`。** 新增模块必须改 Dockerfile。

后续 agent 若发现上述条目被新代码推翻，删除或改写。
