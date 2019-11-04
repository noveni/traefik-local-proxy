# Traefik Reverse Proxy for local develpment

Traefik v2.0

## Config to add to docker-compose

```yaml
version: "3"
services:
  my-container:
    # ...
    labels:
      - traefik.enable=true
      - traefik.docker.network=traefik_webgateway
      - traefik.http.routers.my-container.rule=Host(`mydomain.com`)
      - traefik.http.routers..my-container.entrypoints=web

networks:
  web:
    external:
      name: traefik_webgateway
```
