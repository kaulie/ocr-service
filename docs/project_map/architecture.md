# 服务架构

```
调用方（Brain / character-service）
        │  仅 127.0.0.1
        ▼
  main.py  GET /health
           POST /v1/ocr   JSON base64 / multipart / raw bytes
        │
        ├─ cache.py   sha256(image + language + options + model_version)
        └─ engine.py  PaddleOCR PP-OCRv5_server
```

容器内听 `0.0.0.0:9188`，compose **只映射** `127.0.0.1:9188:9188`。宿主机 Brain 用 `http://127.0.0.1:9188`。

## API

见根 [`README.md`](../../README.md)。响应含 `engine` / `model` / `model_version` / `language` / `text` / `blocks[]`（bbox + confidence）。

## 存储

- 结果缓存卷 `ocr-cache` → `/data/ocr-cache`
- 模型卷 `ocr-models` → `/root/.paddleocr`
- 无 SQLite、无 Asset 库
