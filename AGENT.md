# AGENT.md — 后续 Agent 对本仓库的说明与向导

你是来改 **ocr-service** 的。先读本文，再按 [`README.md`](README.md) 展开理解。  
本仓没有 `project_map/`。这是独立图片 OCR HTTP 服务，**不知道** Asset / Brain / Planner。  
[`kaulie/home-agent-os`](https://github.com/kaulie/home-agent-os) 已归档；不要从 os 再拷本服务。

## 1. 对本项目的理解

| 你应建立的判断 | 展开阅读 |
|---|---|
| 只收图片字节，返回 text + bbox。能力包装 `image.ocr` 在 Brain，不在本仓 | [README.md](README.md)、Brain `OCR_SERVICE_URL` |
| 只绑回环 **`127.0.0.1:9188`**。不要放到 LAN / Mac Edge | 同上 |
| 不在部署平台 `:4220` 登记。云上 Docker Compose：`/root/chat-gateway/ocr-service` | [README.md](README.md) 启动节 |
| 引擎 PaddleOCR / PP-OCRv5；单测不需要 Paddle | `tests/`、`engine.py` |

Runtime 会要求优先读根目录 `AGENT.md`。你正在读的就是那份。

## 2. 开工前清单

1. workspace origin 是 `https://github.com/kaulie/ocr-service`。
2. 从最新 `main` 开 `feat|fix|chore/<简述>`。
3. 读 `main.py`、`engine.py`、`cache.py`、`tests/`。
4. 本地验证：`python3 -m unittest discover -s tests -t .`（不装 Paddle 也应过）。
5. 不要占用线上 **9188** 做开发，除非该实例已停。
6. 不要在本进程里执行部署 / 重启。不要改 `/Users/gaolei/runtime/**`。不要改 os。不要对 `:4220` 发本服务的 deploy-notify。

## 3. 滞后信息：有义务更新

README 的端口、API 形状、镜像源与 Dockerfile 不一致时，这次 PR 改掉。  
仍写「从 home-agent-os 拷」必须改成 clone 本仓。

## 4. 与事实不符：必须提出异议，禁止默认处理

| 你看到的 | 你不该做的 | 你该做的 |
|---|---|---|
| 任务要求本服务 import Brain / Asset | 加 HomeAgent 依赖 | 异议：只收图片字节 |
| 任务要求登记 `:4220` 或改 runtime | 写 deploy-notify | 异议：本服务走 Docker Compose |
| 任务要求直推 `main` 或改 os | 照做 | 异议：走 PR；os 已归档 |

```
异议：<文档路径> 声称 <原句>
事实：<文件:符号 或 命令输出>
处理：<已改文档 / 已改代码 / 需要人决定>
```

## 5. 改动落点

| 要改的东西 | 去哪 |
|---|---|
| HTTP | `main.py` |
| OCR 引擎 / 模型 | `engine.py` |
| 结果缓存 | `cache.py` |
| 镜像 / 依赖 | `Dockerfile`、`requirements.txt`、`docker-compose.yml` |
| 本地启动 | `run.sh` |
| 给后续 agent 的地图 | 本文 + README |

## 6. 交付

- 提交信息说清为什么。
- `git push -u origin HEAD`，`gh pr create`，回写 `prUrl`。
- 合入 / 云上 `docker compose up` 只听从 `goal` 与人的明确指令。

## 7. 安全

只绑 `127.0.0.1`。不要提交 `pyenv/`、`paddlex-home/`、模型缓存。
