# Docker Cheatsheet

> Docker builds, packages, and runs applications in portable containers.

## Table of Contents
- [Images](#images)
- [Containers](#containers)
- [Build](#build)
- [Volumes](#volumes)
- [Networks](#networks)
- [Docker Compose](#docker-compose)
- [Registry](#registry)
- [System & Prune](#system--prune)
- [Inspect & Logs](#inspect--logs)

## Images

| Command | Description |
| --- | --- |
| `docker image ls` | List local images. |
| `docker pull IMAGE:TAG` | Download an image from a registry. |
| `docker image rm IMAGE` | Remove a local image. |
| `docker image tag SOURCE TARGET` | Create an additional tag for an image. |
| `docker image history IMAGE` | Show an image's layer history. |
| `docker image save -o image.tar IMAGE` | Save an image as a tar archive. |
| `docker image load -i image.tar` | Load an image from a tar archive. |

## Containers

| Command | Description |
| --- | --- |
| `docker ps` | List running containers. |
| `docker ps -a` | List all containers including stopped ones. |
| `docker run IMAGE` | Create and start a container from an image. |
| `docker run -d --name NAME IMAGE` | Run a named container in the background. |
| `docker run -p 8080:80 IMAGE` | Publish a container port to the host. |
| `docker run -e KEY=VALUE IMAGE` | Set an environment variable in a container. |
| `docker start CONTAINER` | Start an existing stopped container. |
| `docker stop CONTAINER` | Gracefully stop a running container. |
| `docker restart CONTAINER` | Restart a container. |
| `docker rm CONTAINER` | Remove a stopped container. |

## Build

| Command | Description |
| --- | --- |
| `docker build -t IMAGE:TAG .` | Build an image from the current directory. |
| `docker build -f Dockerfile.prod -t IMAGE:TAG .` | Build using a specified Dockerfile. |
| `docker build --build-arg NAME=VALUE -t IMAGE .` | Pass a build argument to a Dockerfile. |
| `docker build --no-cache -t IMAGE .` | Build without using cached layers. |
| `docker buildx build --platform linux/amd64,linux/arm64 -t IMAGE --push .` | Build and push a multi-platform image. |
| `docker commit CONTAINER IMAGE:TAG` | Create an image from a container's filesystem. |

## Volumes

| Command | Description |
| --- | --- |
| `docker volume ls` | List Docker volumes. |
| `docker volume create VOLUME` | Create a named volume. |
| `docker run -v VOLUME:/data IMAGE` | Mount a named volume into a container. |
| `docker run -v $(pwd):/app IMAGE` | Bind-mount the current directory into a container. |
| `docker volume inspect VOLUME` | Show volume metadata and mount location. |
| `docker volume rm VOLUME` | Remove an unused volume. |

## Networks

| Command | Description |
| --- | --- |
| `docker network ls` | List Docker networks. |
| `docker network create NETWORK` | Create a user-defined bridge network. |
| `docker run --network NETWORK IMAGE` | Run a container attached to a network. |
| `docker network connect NETWORK CONTAINER` | Attach an existing container to a network. |
| `docker network disconnect NETWORK CONTAINER` | Detach a container from a network. |
| `docker network inspect NETWORK` | Show network configuration and connected containers. |
| `docker network rm NETWORK` | Remove an unused network. |

## Docker Compose

| Command | Description |
| --- | --- |
| `docker compose up` | Create and start services from a Compose file. |
| `docker compose up -d` | Start Compose services in the background. |
| `docker compose down` | Stop and remove Compose services and networks. |
| `docker compose ps` | List Compose service containers. |
| `docker compose logs -f` | Stream logs from all Compose services. |
| `docker compose exec SERVICE sh` | Open a shell in a running Compose service. |
| `docker compose build` | Build images for Compose services. |
| `docker compose pull` | Pull images for Compose services. |
| `docker compose restart SERVICE` | Restart a Compose service. |

## Registry

| Command | Description |
| --- | --- |
| `docker login REGISTRY` | Authenticate with a container registry. |
| `docker logout REGISTRY` | Remove registry credentials from the local client. |
| `docker push IMAGE:TAG` | Push an image tag to its registry. |
| `docker pull IMAGE:TAG` | Pull an image tag from its registry. |
| `docker search TERM` | Search Docker Hub for images. |
| `docker image tag IMAGE REGISTRY/REPOSITORY:TAG` | Tag an image for a registry repository. |

## System & Prune

| Command | Description |
| --- | --- |
| `docker system df` | Show Docker disk usage. |
| `docker system prune` | Remove unused stopped containers, networks, and cache. |
| `docker system prune -a` | Also remove unused images. |
| `docker container prune` | Remove all stopped containers. |
| `docker image prune` | Remove dangling images. |
| `docker volume prune` | Remove unused local volumes. |
| `docker builder prune` | Remove unused build cache. |

## Inspect & Logs

| Command | Description |
| --- | --- |
| `docker inspect CONTAINER` | Show detailed JSON metadata for a container. |
| `docker inspect -f '{{.State.Status}}' CONTAINER` | Print a selected container status field. |
| `docker logs CONTAINER` | Print container logs. |
| `docker logs -f CONTAINER` | Stream container logs. |
| `docker logs --tail 100 CONTAINER` | Print the most recent log lines. |
| `docker exec -it CONTAINER sh` | Open an interactive shell in a container. |
| `docker stats` | Stream CPU, memory, and network usage. |
| `docker top CONTAINER` | Display processes running in a container. |
