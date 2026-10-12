# 项目定位

## 一句话

ocr-service 是独立图片 OCR HTTP 服务：收图片字节，返回 text + bbox。它不知道 HomeAgent Asset、Brain DB、Runtime。

仓库：[`https://github.com/kaulie/ocr-service`](https://github.com/kaulie/ocr-service)  
回环口：`127.0.0.1:9188`

## 它要解决什么

Brain 通过 `OCR_SERVICE_URL`（默认 `http://127.0.0.1:9188`）调用本服务，再包装成能力 `image.ocr`。character-service 也调本机同一口做识字。

## 它不是什么

| 不是 | 谁才是 |
|---|---|
| `image.ocr` 能力声明 / 规划步 | 集市 + Brain |
| 指字几何 | [`character-service`](https://github.com/kaulie/character-service) |
| 平台托管 runtime | Brain / Gateway / 集市（它们才走 `:4220`） |
| os 子树 | [`home-agent-os`](https://github.com/kaulie/home-agent-os) 已归档 |

## 当前形态

- 单进程 `main.py`（stdlib HTTP）
- 引擎 PaddleOCR / PP-OCRv5_server
- 云上 Docker Compose：`container_name: home-agent-ocr`，`restart: unless-stopped`
