# LinkLian Infrastructure

This project provides Redis and Redis HTTP (for testing an Upstash-like HTTP gateway) via Docker Compose.

---

## Prerequisites

- [Docker](https://www.docker.com/) and Docker Compose
- Create the Docker network `linklian-net` once before first use

```bash
docker network create linklian-net
```

---

## Services

| Service | Container | Port (Host -> Container) | Details |
|---|---|---|---|
| Redis | linklian-redis | 6379 -> 6379 | Primary Redis with AOF enabled |
| Redis HTTP | linklian-upstash-redis | 4001 -> 8080 | HTTP gateway for Redis |

---

## Getting Started

```bash
docker compose up -d
```

---

## Using Redis

### Connect via Redis Client

- Host: `localhost`
- Port: `6379`

Example:

```bash
redis-cli -h localhost -p 6379
```

### Connect via HTTP (Redis HTTP)

- Base URL: `http://localhost:4001`
- Token (default): `12345678`

Example with curl:

```bash
curl -X POST "http://localhost:4001" \
	-H "Authorization: Bearer 12345678" \
	-d 'command=PING'
```

> Note: To change the token, update `SRH_TOKEN` in [docker-compose.yml](docker-compose.yml)

---

## Common Commands

```bash
# View logs
docker compose logs -f

# Stop all services
docker compose stop

# Stop and remove containers
docker compose down

# Restart a single service
docker compose restart linklian-redis
```
