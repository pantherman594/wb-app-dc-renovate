FROM python:3.14-slim@sha256:cea0e6040540fb2b965b6e7fb5ffa00871e632eef63719f0ea54bca189ce14a6

# Create non-root user
RUN groupadd -r appuser && useradd -r -g appuser -d /home/appuser -m appuser

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    fuse \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy requirements first for caching
COPY app/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY app/ .

# Set ownership
RUN chown -R appuser:appuser /app /home/appuser

# Expose port
EXPOSE 8080

# Run as non-root user
USER appuser

# Start application
CMD ["python", "main.py"]
