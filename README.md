# Nova Docker — Port 4443 Patch

A patched version of [IRNova/Nova-Server](https://github.com/IRNova/Nova-Server) that runs Nova on port **4443** instead of **443**, so it can coexist with nginx or any other service already using port 443 on the same server.

## What's changed

- `nova-node.sh` — default front port changed from 443 to 4443
- `firstboot.sh` — health check targets port 4443
- `nova-node.sh` — `NOVA_FRONT_PORT=4443` is always written to `agent.env`

## Requirements

- A Linux VPS (Ubuntu/Debian)
- Docker + Docker Compose installed
- Port **4443** open on your firewall

## Install

```bash
git clone https://github.com/mehranghazi/nova-docker-patch.git
cd nova-docker-patch
docker compose up -d --build
docker compose logs -f nova-node
```

Wait a few minutes. When you see `==> Nova node installed and healthy.`, your panel URL and admin password are printed above it.

## Access

The panel runs at:

```
https://YOUR_SERVER_IP:4443/YOUR_SECRET_PATH/
```

> Nova uses a self-signed certificate. In the Nova app, turn on **"My server has no domain"**.

## Stop / Remove

```bash
docker compose down
docker volume rm nova-data nova-cert nova-xray
```

## Update

```bash
git pull
docker compose down
docker compose up -d --build
```
