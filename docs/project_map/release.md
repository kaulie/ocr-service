# 发布细节

本仓库**没有** `build.sh`、没有 `scripts/restart.sh`、没有平台 `outputs/`。

一次「发布」= 把目标 ref 拉到 `/root/chat-gateway/ocr-service`，再 `docker compose up -d --build`。

合入 `main` ≠ 云上容器已换新镜像。首次启动会把 PP-OCRv5 模型下到 cache volume。
