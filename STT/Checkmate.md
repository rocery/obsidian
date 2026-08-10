
Install Docker:
apt update
apt install -y git openssl curl gawk coreutils grep jq
curl -sSL https://get.docker.com/ | CHANNEL=stable sh
systemctl enable --now docker
# Dasboard
Install:
Use root account
mkdir checkmate
cd checkmate
curl -O https://raw.githubusercontent.com/bluewave-labs/checkmate/master/docker/docker-compose.yaml
cat docker-compose.yaml
openssl rand -hex 32 --> copy the string to docker-compose.yaml and edit JWT
- CLIENT_HOST=${CLIENT_HOST:-http://localhost:52345}
- JWT_SECRET=${JWT_SECRET:?set JWT_SECRET in your environment}
docker compose up -d
open host

# Monitoring Agent Checkmate
mkdir capture
cd capture
nano compose.yml
```
services:
  capture:
    image: ghcr.io/bluewave-labs/capture:latest
    container_name: capture
    restart: unless-stopped

    ports:
      - "59232:59232"

    environment:
      API_SECRET: "SECRET_CODE"

    volumes:
      - /etc/os-release:/etc/os-release:ro
```
docker compose up -d
sudo ufw allow 59232/tcp
Infrastructure -> http://192.168.10.50:59232 /api/v1/metrics or /health
