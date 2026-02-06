## OpenCloud - Self-hosted Cloud Storage

OpenCloud with Collabora Online office integration, configured for use behind an external reverse proxy.

### Services

| Service       | Container Name          | Port  | Description                    |
| ------------- | ----------------------- | ----- | ------------------------------ |
| opencloud     | opencloud-app           | 62000 | OpenCloud server (proxy: 9200) |
| collaboration | opencloud-collaboration | 62001 | WOPI server (collaboration)    |
| collabora     | opencloud-collabora     | 62002 | Collabora Online (office)      |

All ports bind to `172.17.0.1` for access via the nginx proxy.

### Requires composemgr to be installed

```shell
sudo bash -c "$(curl -q -LSsf "https://github.com/composemgr/installer/raw/main/install.sh")" && sudo composemgr install installer
```

### Install docker compose files

```shell
composemgr install opencloud
```

### Edit .env

```shell
$EDITOR "$HOME/.config/myscripts/composemgr/docker/opencloud/.env"
```

At minimum, set these variables:

- `OC_DOMAIN` - your OpenCloud domain (e.g. `cloud.example.com`)
- `COLLABORA_DOMAIN` - your Collabora domain (e.g. `collabora.example.com`)
- `WOPISERVER_DOMAIN` - your WOPI server domain (e.g. `wopiserver.example.com`)
- `INITIAL_ADMIN_PASSWORD` - admin password (must be set before first start)

### Edit app.env - will overwrite defaults from .env

```shell
$EDITOR "$HOME/.config/myscripts/composemgr/docker/opencloud/app.env"
```

### Pull the containers

```shell
composemgr --dir "$HOME/.config/myscripts/composemgr/docker/opencloud" pull
```

### Start the stack

```shell
composemgr --dir "$HOME/.config/myscripts/composemgr/docker/opencloud" up
```

### Get the logs for the stack

```shell
composemgr --dir "$HOME/.config/myscripts/composemgr/docker/opencloud" logs
```

### Reverse Proxy Configuration

Your external proxy needs to route these domains:

- `OC_DOMAIN` -> `172.17.0.1:62000`
- `WOPISERVER_DOMAIN` -> `172.17.0.1:62001`
- `COLLABORA_DOMAIN` -> `172.17.0.1:62002`

All three domains require valid TLS certificates managed by your proxy.

### References

- [OpenCloud Documentation](https://docs.opencloud.eu)
- [OpenCloud Compose Repository](https://github.com/opencloud-eu/opencloud-compose)
- [Collabora Online](https://www.collaboraonline.com)
