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
This command builds the image defined in `compose.yaml`.

---

## Start the Service
Run:
```bash
docker compose up -d
```
This command starts the service in detached mode.
To start it in the foreground instead, run:
```bash
docker compose up
```

---

## Check Running Services
Run:
```bash
docker compose ps
```
This shows the current status of the services defined in the Compose project.

---

## Read Logs
Run:
```bash
docker compose logs
```
To follow logs in real time:
```bash
docker compose logs -f toolbox
```

---

## Enter the Running Container
Run:
```bash
docker compose exec toolbox sh
```
Once inside the container, you can test a few commands such as:
```bash
pwd
ls -la
env | grep LAB_MESSAGE
which curl
which bash
cat /usr/local/bin/welcome.sh
```
Exit the container shell with:
```bash
exit
```

---

## Stop and Clean Up
Run:
```bash
docker compose down
```
This stops and removes the containers and networks created by Docker Compose for this project.

---

## Useful Daily Commands
### Rebuild after changing the Dockerfile
```bash
docker compose build
```
### Rebuild and restart
```bash
docker compose up -d --build
```
### Stop services
```bash
docker compose down
```
### View container logs
```bash
docker compose logs -f
```
### Open a shell in the running container
```bash
docker compose exec toolbox sh
```

---

## Notes
This repository is intentionally simple and educational.
The goal is to build strong fundamentals before moving to more advanced and production-like setups.
