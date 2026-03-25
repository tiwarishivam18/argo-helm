FROM python:3.12-slim AS builder
WORKDIR /app

COPY src/requirements.txt .


RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

RUN pip install --no-cache-dir -r requirements.txt

COPY src ./src/


FROM python:3.12-slim
WORKDIR /app

COPY --from=builder /opt/venv /opt/venv
COPY --from=builder /app /app

ENV PATH="/opt/venv/bin:$PATH"

RUN useradd -m appuser && chown -R appuser:appuser /app
USER appuser

EXPOSE 5000

CMD ["python", "src/app.py"]
