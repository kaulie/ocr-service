# 开发流程

origin：`https://github.com/kaulie/ocr-service`。从最新 `origin/main` 开短命分支，PR 回 `main`。禁止直推 / force push `main`。

1. 先读 [`../../AGENT.md`](../../AGENT.md) 与本目录。
2. HTTP 改 `main.py`；引擎改 `engine.py`；缓存改 `cache.py`。
3. 新增 `.py` 必须同步 `Dockerfile` 的 `COPY`。
4. 不要 import Brain / Asset。
5. 不要对 `:4220` 发本服务。不要改 os。

```bash
python3 -m unittest discover -s tests -t .
```

不装 Paddle 也应过。不要提交 `pyenv/`、`paddlex-home/`、模型缓存。
