# 技术栈

| 项 | 事实 |
|---|---|
| 语言 | Python 3.10（镜像 `python:3.10-bookworm` via DaoCloud） |
| HTTP | stdlib（`main.py`） |
| 引擎 | paddlepaddle==3.0.0，paddleocr>=3.0.0 |
| 模型 | PP-OCRv5_server（`OCR_MODEL_VERSION=PP-OCRv5`） |
| 系统库 | libgl1、libglib2.0-0、libgomp1 |
| PyPI | 清华镜像（Dockerfile） |
| Debian | Aliyun（Dockerfile） |
| 单测 | `unittest`，`tests/`；**不需要**装 Paddle |
| 本地 requirements.txt | 几乎空：运行时依赖在镜像里 |

无 `build.sh`。无 Flask。无 HomeAgent SDK。
