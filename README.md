## 👋 Welcome to opencloud 🚀

Self-hosted cloud storage with Collabora Online office integration

## 📋 Description

Self-hosted cloud storage with Collabora Online office integration

## 🚀 Services

- **server**: opencloudeu/opencloud-rolling:latest
- **collaboration**: opencloudeu/opencloud-rolling:latest
- **collabora**: collabora/code:25.04.7.1.1

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/opencloud/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/opencloud" ~/.local/srv/docker/opencloud
cd ~/.local/srv/docker/opencloud
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install opencloud
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
BASE_DOMAIN_NAME=example.com
BASE_HOST_NAME=opencloud.example.com
SERVICE_USER=1000
SERVICE_GROUP=1000
APP_ADMIN_PASS=replace-with-a-random-password
COLLABORA_ADMIN_USER=admin
COLLABORA_ADMIN_PASS=replace-with-a-random-password
OC_LOG_LEVEL=info
COLLABORATION_LOG_LEVEL=info
EMAIL_SERVER_PORT=587
EMAIL_SERVER_HOST=172.17.0.1
EMAIL_SERVER_MAIL_FROM=no-reply@example.com
EMAIL_SERVER_LOGIN_NAME=replace-with-your-smtp-username
EMAIL_SERVER_LOGIN_PASS=replace-with-your-smtp-password
CLOUDFLARE_ZONE_NAME=example.com
CLOUDFLARE_TUNNEL_ID=replace-with-your-tunnel-id
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64282` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64282

## 📂 Volumes

- `./volumes/config/opencloud` - Configuration
- `./volumes/config/opencloud/apps` - App assets
- `./volumes/data/opencloud` - Application data

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f server
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
