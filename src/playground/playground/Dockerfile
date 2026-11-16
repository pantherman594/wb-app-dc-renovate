FROM golang:1.27-alpine@sha256:70bd7ddea8b6cbe5d6943cde279d6b67feb10cc924fb9100d1d8757c1575b280 AS build

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download
COPY . .
 
RUN go build -o /playground .

FROM alpine:latest

# Install Node.js, npm, Docker CLI, docker-compose, buildx, ttyd, bash, and devcontainer CLI
RUN apk add --no-cache nodejs npm docker-cli docker-cli-compose docker-cli-buildx ttyd bash && \
    npm install -g @devcontainers/cli

RUN addgroup -S playground -g 1001 && adduser -S playground -u 1001 -G playground

WORKDIR /workspace
COPY --chown=playground:playground --from=build /playground /playground

# Create startup script to run ttyd in background and playground in foreground
RUN cat > /start.sh <<'EOF'
#!/bin/sh
ttyd --writable --port 7681 --base-path /_shell bash &
exec /playground
EOF

RUN chmod +x /start.sh

USER playground

EXPOSE 8080 7681

CMD [ "/start.sh" ]
