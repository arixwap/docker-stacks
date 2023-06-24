# Docker stack for local or production environment

**List of available services**

- **Traefik**: router for incoming traffic to the appropriate docker containers
- **Portainer**: web UI for docker stacks, like _Docker Desktop_
- **MariaDB**: alternative MySQL database
- **phpMyAdmin**: web UI for MariaDB database
- **Postgres**: another open source object-relational database
- **pgAdmin**: web UI for postgres
- **Adminer**: web UI for MariaDB & Postgres database management
- **MongoDB**: non-relational document database that provides support for JSON-like storage
- **Mongo Express**: web UI for mongodb
- **Redis**: cache server, in-memory, key-value data store.
- **phpRedisAdmin**: simple web interface to manage Redis databases.

## Getting Started

```
# Go inside core folder
cd core
```

```
# Create docker network called `proxy`
docker network create proxy
```

```
# Set env
cp .env.example .env

# you can also set port, domains and other services value via .env files
```

```
# Run docker compose
docker compose up -d

# Run specific service using args `--profile`
docker compose --profile mariadb up -d

# Or run all services
docker compose --profile all up -d
```

Put your application inside folder `apps/`.
Run it using docker compose with `traefik labels`.

Example `docker-compose.yml`

```
services:
  example:
    image: example-image:latest
    labels:
      - traefik.enable=true
      - traefik.docker.network=proxy
      # Usually in local without https
      - traefik.http.routers.example.entrypoints=web
      # In production if using https
      # - traefik.http.routers.example.entrypoints=websecure
      - traefik.http.routers.example.rule=Host(`example.com`,`www.example.com`)
    networks:
      - proxy
networks:
  proxy:
    external: true
```

## TODO List

- [ ] Traefik: env http auth

---

This is custom forked repository from https://github.com/rafrasenberg/docker-traefik-portainer

You can check original Detailed explanation here: https://rafrasenberg.com/docker-compose-traefik-v2
