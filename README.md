# compose-n8n

This repository contains one Docker Compose configuration with profiles:

- The `container` profile runs n8n, PostgreSQL, and Redis in containers.
- The `host` profile runs n8n in a container and connects it to PostgreSQL and Redis on the host machine.

## Prerequisites

- Docker
- Docker Compose

## Setup

1. Clone this repository or copy the files.

2. Create and edit the single `.env` file:
   ```bash
   cp .env.example .env
   ```

   - Generate a secure `N8N_ENCRYPTION_KEY` (you can use `openssl rand -base64 32`)
   - Set database name, user, and password
   - For the host configuration, `host.docker.internal` is available on Docker Desktop for macOS/Windows; on Linux, set `DB_POSTGRESDB_HOST` and `QUEUE_BULL_REDIS_HOST` to host addresses reachable from the container
   - Ensure host PostgreSQL and Redis accept connections from Docker
   - Configure authentication credentials
   - Change `N8N_PORT_HOST` if you want n8n to run on a different port

3. Choose one mode and start it:

   **Use PostgreSQL and Redis on the host machine:**
   ```bash
   docker compose --profile host up -d n8n-host
   ```

   **Run PostgreSQL and Redis in Docker (no host database needed):**
   ```bash
   docker compose --profile container up -d
   ```

4. Access n8n at http://localhost:5678 (or the port you set in N8N_PORT_HOST)

5. Log in with the credentials set in `.env`.

Only run one profile at a time; both n8n services use the same host port and data volume. Run `docker compose down` before switching modes. For the host mode, make sure the database and Redis already exist and are reachable from Docker.

## Files

- `docker-compose.yml`: Compose configuration for both profiles
- `.env.example`: The single environment template for both configurations
- `.env`: Environment variables shared by both configurations
- `.gitignore`: Git ignore rules (excludes .env and other sensitive/temporary files)

## Volumes

- `n8n_data`: Stores n8n configuration and workflows.
- `postgres_data`: Stores PostgreSQL data in the all-container configuration.
- `redis_data`: Stores Redis data.

## Stopping the Services

To stop the selected profile:

```bash
docker compose down
```

To stop and remove volumes (this will delete n8n and, for the all-container configuration, PostgreSQL/Redis data):

```bash
docker compose down -v
```
