# Stage 1: Build
FROM ghcr.io/astral-sh/uv:0.11.0-python3.13-trixie-slim AS builder

ENV UV_COMPILE_BYTECODE=1
ENV UV_PYTHON_DOWNLOADS=never

WORKDIR /app
RUN uv venv .venv
RUN --mount=type=cache,target=/root/.cache/uv \
    uv pip install --python .venv/bin/python \
  "git+https://github.com/<DEIN_GITHUB_NAME>/grocy-mcp.git@d0b00014c1ca4cca09f1c6c05527a5f92fd3f5c4"

# Stage 2: Runtime
FROM python:3.13-slim

COPY --from=builder /app/.venv /app/.venv
ENV PATH="/app/.venv/bin:$PATH"

COPY start.py /start.py

CMD ["python3", "/start.py"]
