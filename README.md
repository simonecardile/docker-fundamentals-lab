# docker-fundamentals-lab

A public learning repository built to practice Docker fundamentals through a small multi-service lab.

## Goal

This repository was created to learn Docker hands-on, focusing on:

- custom images with `Dockerfile`
- multi-service applications with Docker Compose
- environment variables
- bind mounts
- named volumes
- custom networks
- healthchecks
- service startup order with `depends_on` and `service_healthy`
- basic troubleshooting commands

## Tech Stack

- Docker Desktop
- WSL 2
- Docker Compose
- Alpine Linux
- Nginx

## Repository Structure

```text
docker-fundamentals-lab/
├─ docker/
│  └─ toolbox/
│     └─ Dockerfile
├─ scripts/
│  └─ welcome.sh
├─ lab/
│  └─ web/
│     └─ index.html
├─ .dockerignore
├─ .env.example
├─ .gitignore
├─ compose.yaml
└─ README.md
```

## Services

### toolbox
A custom image based on Alpine Linux used as a learning container.

It includes:
- `bash`
- `curl`
- `bind-tools`

### web
A simple Nginx container serving a static HTML page.

## Concepts Covered

### Dockerfile
The `toolbox` image is built from a custom `Dockerfile`.

### Docker Compose
The project uses `compose.yaml` to define services, volumes, networks, and startup dependencies.

### Environment Variables
Environment values are loaded from a local `.env` file.

### Bind Mount
The whole repository is mounted into the container at:

```text
/workspace/app
```

This allows real-time file changes from the host.

### Named Volume
The `toolbox_data` volume is mounted at:

```text
/data
```

This is used to demonstrate persistent Docker-managed storage.

### Network Between Containers
Both services share a custom bridge network:

```text
dockerfundamentalslab_lab_net
```

The `toolbox` container can reach the `web` service by hostname:

```bash
curl http://web
```

### Healthcheck
The `web` service exposes a healthcheck that verifies that Nginx is responding locally.

### Service Startup Order
`toolbox` depends on `web` with:

```yaml
depends_on:
  web:
    condition: service_healthy
```

This means `toolbox` starts only after `web` is healthy.

## Requirements

- Docker Desktop installed and running
- WSL 2 enabled
- Docker Desktop integration enabled for your WSL distribution
- VS Code recommended
- source code stored inside the Linux filesystem of WSL

## Local Setup

Create your local environment file:

```bash
cp .env.example .env
```

Then start the project:

```bash
docker compose up -d
```

## Useful Commands

### Show the resolved Compose configuration
```bash
docker compose config
```

### Build images
```bash
docker compose build
```

### Start services
```bash
docker compose up -d
```

### Start services and rebuild first
```bash
docker compose up -d --build
```

### Stop services without removing containers
```bash
docker compose stop
```

### Start existing stopped containers
```bash
docker compose start
```

### Restart services
```bash
docker compose restart
```

### Tear down services and network
```bash
docker compose down
```

### Tear down services, network, and named volumes
```bash
docker compose down -v
```

### Check service status
```bash
docker compose ps
```

### Check logs
```bash
docker compose logs
docker compose logs -f
```

### Open a shell inside toolbox
```bash
docker compose exec toolbox sh
```

## Troubleshooting

### Validate the Compose configuration
```bash
docker compose config >/dev/null && echo "CONFIG OK"
```

### Inspect container health
```bash
docker inspect dockerfundamentalslab-web-1 --format '{{json .State.Health}}'
```

### List containers
```bash
docker ps
docker ps -a
```

### List Docker resources
```bash
docker images
docker volume ls
docker network ls
```

## What I learned in this repository

- the difference between an image and a container
- how Docker builds an image from a `Dockerfile`
- how Docker Compose defines and runs multiple services
- how bind mounts differ from named volumes
- how containers communicate over a Docker network
- how healthchecks work
- how `depends_on` with `service_healthy` affects startup order
- how to troubleshoot with `config`, `ps`, `logs`, and `inspect`

## Notes

This repository is intentionally small and educational.
The goal is not production readiness, but strong operational fundamentals.
