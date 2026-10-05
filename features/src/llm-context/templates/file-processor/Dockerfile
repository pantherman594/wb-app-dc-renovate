FROM python:3.11-slim@sha256:6f31d6e9ba2b0a787a3f81c37b004155b87b9efa1b771182bd550c1615745be5

RUN groupadd -r appuser && useradd -r -g appuser -d /home/appuser -m appuser

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl fuse \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Create directories for file processing
RUN mkdir -p /app/uploads /app/processed /app/schemas && \
    chown -R appuser:appuser /app

COPY app/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app/ .
RUN chown -R appuser:appuser /app /home/appuser

EXPOSE 8080
USER appuser

CMD ["python", "main.py"]
