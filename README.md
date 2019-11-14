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
      - traefik.docker.network=local_traefik_webgateway
      - traefik.http.routers.my-container.rule=Host(`mydomain.test`,`mydomain.locahost`,`mydomain.localdev`)
      - traefik.http.routers.my-container.entrypoints=http
      - traefik.http.routers.my-container-secure.rule=Host(`mydomain.test`,`mydomain.locahost`,`mydomain.localdev`)
      - traefik.http.routers.my-container-secure.entrypoints=https
      - traefik.http.routers.my-container-secure.tls=true

networks:
  web:
    external:
      name: local_traefik_webgateway
```

The name of the externals network it's really important.
It can be changed in the traefik docker-compose file.
