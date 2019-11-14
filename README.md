# Traefik Reverse Proxy for local development

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

## Adding SSL to docker and Traefik

In the `devcerts/`:

```sh
mkcert mydomain.localdev "*.mydomain.localdev"
```

Using wildcards for subdomain

In `config/dynamic.toml` file, add the following instructions for the newly generated certificate

```toml
[[tls.certificates]]
  certFile = "/etc/certs/mydomain.localdev.pem"
  keyFile = "/etc/certs/mydomain.localdev-key.pem"
```
