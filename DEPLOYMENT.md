# Simple Deployment (Docker Compose Only)

This project can run on a fresh server with only Docker + Docker Compose.

## Requirements

- Docker Engine installed
- Docker Compose plugin installed (`docker compose` command works)
- Open TCP port `3002` on the server firewall

> Note: This repo currently maps `3002 -> 3001` in `compose.yaml`.
> If you want standard port `3001`, change `compose.yaml` line:
> `- "3002:3001"` to `- "3001:3001"`.

## Deploy

1. Put this repo on your server (clone or upload it).
2. Go into the project folder.
3. Start the app:

```bash
docker compose up -d --build
```

4. Check status:

```bash
docker compose ps
```

5. Open in browser:

```text
http://YOUR_SERVER_IP:3002
```

On first open, create your admin account in the setup page.

## Useful Commands

### View logs

```bash
docker compose logs -f --tail=200
```

### Restart

```bash
docker compose restart
```

### Stop

```bash
docker compose down
```

### Update after new commits

```bash
git pull
docker compose up -d --build
```

## Data Persistence

Your monitoring data is stored in:

```text
./data
```

This is mounted to `/app/data` inside the container, so data remains after restart/redeploy.

### Simple backup example

```bash
tar -czf uptime-kuma-data-backup-$(date +%F).tar.gz data/
```
