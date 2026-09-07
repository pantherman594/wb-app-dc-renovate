FROM python:3.11-slim@sha256:9534e5a8e315485d4061ed659af0fd78a284c015f9b73661b41d6bab25604534

RUN groupadd -r appuser && useradd -r -g appuser -d /home/appuser -m appuser

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl fuse \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY app/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app/ .
RUN chown -R appuser:appuser /app /home/appuser

EXPOSE 8501
USER appuser

CMD ["streamlit", "run", "main.py", "--server.port=8501", "--server.address=0.0.0.0"]
