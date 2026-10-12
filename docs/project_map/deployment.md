# 部署细节

## 谁负责部署

**不是** `:4220`。云上目录 `/root/chat-gateway/ocr-service`，Docker Compose：

```bash
git clone https://github.com/kaulie/ocr-service.git /root/chat-gateway/ocr-service
cd /root/chat-gateway/ocr-service
docker compose up -d --build
curl -sS http://127.0.0.1:9188/health
```

- 不要改 systemd。
- 不要对本服务发 `POST :4220/api/deploy-notify`。
- 不要改 `/Users/gaolei/runtime/**`。
- 合入 / `docker compose up` 只听从 `goal` 与人的明确指令。

容器：`home-agent-ocr`，`mem_limit: 4g`，`restart: unless-stopped`。

Brain `.env`：`OCR_SERVICE_URL=http://127.0.0.1:9188`。

## 端口

只绑回环 **9188**。本机开发不要占用线上 9188，除非该实例已停。
