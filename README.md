# compose-n8n

This repository contains a Docker Compose setup for deploying n8n, a workflow automation tool.

## Prerequisites

- Docker
- Docker Compose

## Setup

1. Clone this repository or copy the files.

2. Copy the example environment file and configure your settings:

   ```bash
   cp .env.example .env
   ```

3. Edit the `.env` file to set your own values:
   - Generate a secure `N8N_ENCRYPTION_KEY` (you can use `openssl rand -base64 32`)
   - Set secure database passwords
   - Configure authentication credentials
   - Change `N8N_PORT_HOST` if you want n8n to run on a different port

4. Run the following command to start the services:

   ```bash
   docker-compose up -d
   ```

5. Access n8n at http://localhost:5678 (or the port you set in N8N_PORT_HOST)

6. Log in with the credentials set in your `.env` file.

## Files

- `docker-compose.yml`: Main Docker Compose configuration
- `.env.example`: Example environment variables file
- `.env`: Your environment variables (copy from .env.example and customize)
- `.gitignore`: Git ignore rules (excludes .env and other sensitive/temporary files)

## Volumes

- `n8n_data`: Stores n8n configuration and workflows.
- `postgres_data`: Stores database data.
- `redis_data`: Stores Redis data.

## Stopping the Services

To stop the services:

```bash
docker-compose down
```

To stop and remove volumes (this will delete all data):

```bash
docker-compose down -v
```
