# docker-fundamentals-lab
- building custom images with a `Dockerfile`
- running containers with Docker Compose
- using environment variables
- reading logs
- entering running containers
- stopping and cleaning up services

---

## Current Scope
At the current stage, this lab includes:
- a custom Docker image based on Alpine Linux
- a simple startup script copied into the image
- a `compose.yaml` file to build and run the service
- a `.env` file for environment variables
- basic Docker Compose commands for daily usage

---

## Repository Structure
```text
docker-fundamentals-lab/
├─ docker/
│  └─ toolbox/
│     └─ Dockerfile
├─ scripts/
│  └─ welcome.sh
├─ .env
├─ .gitignore
├─ compose.yaml
└─ README.md
```

---

## Requirements
Before using this repository, make sure you have:
- Docker Desktop installed and running
- WSL 2 enabled
- Docker Desktop integration enabled for your WSL distribution
- VS Code (recommended)
- A Linux shell inside WSL for running commands
Recommended setup:
- source code stored inside the Linux filesystem (WSL), not under `C:\`
- commands run from the VS Code integrated terminal connected to WSL

---

## Concepts Covered in This Step
### Image
An image is the build artifact created from a `Dockerfile`.
It contains the filesystem, packages, tools, and default startup command.
### Container
A container is a running instance of an image.
### Dockerfile
A `Dockerfile` defines how the image is built.
### Docker Compose
Docker Compose defines and runs services using a YAML file.
### Environment Variables
The `.env` file is used to provide values to the Compose configuration and the running container.

---

## Files Explained
### `docker/toolbox/Dockerfile`
Builds a small custom image based on Alpine Linux and installs a few useful tools:
- `bash`
- `curl`
- `bind-tools`
It also copies a startup script into the image and runs it when the container starts.
### `scripts/welcome.sh`
A small shell script used to confirm that:
- the container is running
- environment variables are available
- the working directory is correct
### `.env`
Stores simple environment variables used by Docker Compose.
### `compose.yaml`
Defines the `toolbox` service and tells Docker Compose how to build and run it.

---

## Build the Image
Run:
```bash
docker compose build
```

---

## Start the Service
Run:
```bash
docker compose up -d
```
