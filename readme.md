# LinkLian Infrastructure

## Database (PostgreSQL 18)

This project runs PostgreSQL 18 via Docker Compose with separate configurations for **dev** and **prod** environments.

---

## Prerequisites

- [Docker](https://www.docker.com/) and Docker Compose installed
- Create the `linklian-net` Docker network once before starting:

```bash
docker network create linklian-net
```

---

## Environment Variables

Create a `.env` file in the same directory as the `docker-compose.yml` you intend to run:

```env
DB_USER=your_username
DB_PASSWORD=your_password
DB_NAME=your_database_name
```

---

## Starting the Database

### Development

```bash
cd dev
docker compose up -d
```

- Container name: `linklian-database-dev`
- Port: `5412` (host) → `5432` (container)
- Data volume: `./dev/databasepg`

### Production

```bash
cd prod
docker compose up -d
```

- Container name: `linklian-database-prod`
- Port: `5402` (host) → `5432` (container)
- Data volume: `./prod/databasepg`

---

## Connecting to the Database

| Environment | Host      | Port |
|-------------|-----------|------|
| Dev         | localhost | 5412 |
| Prod        | localhost | 5402 |

Example connection string:

```
postgresql://<DB_USER>:<DB_PASSWORD>@localhost:<PORT>/<DB_NAME>
```

---

## Common Commands

```bash
# View logs
docker compose logs -f database

# Stop the container
docker compose stop

# Stop and remove the container
docker compose down

# Restart the container
docker compose restart database
```
