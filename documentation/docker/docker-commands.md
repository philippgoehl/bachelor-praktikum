# Docker CLI

```bash
docker --version # Check Docker version
docker info # Display system-wide information

# List commands
docker images # List all images
docker ps # List all running containers
docker ps -a # List all containers (running and stopped)

# Build and run commands
docker pull <image-name> # Pull an image from a registry
docker run <image-name> # Run a container from an image
docker run -d <image-name> # Run a container in detached mode
docker stop <container-name> # Stop a container
docker start <container-name> # Start a container
docker restart <container-name> # Restart a container

# Delete commands
docker rmi <image-name> # Remove an image
docker rm <container-name> # Remove a container
docker rm <container-id> # Remove a container by ID
docker rm $(docker ps -a -q) # Remove all containers
docker rmi $(docker images -q) # Remove all images
docker system prune # Remove all stopped containers, all dangling images, and all unused networks
docker container prune # Remove all stopped containers
docker image prune # Remove all dangling images
docker volume prune # Remove all unused volumes
docker network prune # Remove all unused networks

# Exec commands in a running container
docker exec <container-name> <command> # Execute a command in a running container
```
