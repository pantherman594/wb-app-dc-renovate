FROM golang:1.26-alpine@sha256:0178a641fbb4858c5f1b48e34bdaabe0350a330a1b1149aabd498d0699ff5fb2 AS build

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
