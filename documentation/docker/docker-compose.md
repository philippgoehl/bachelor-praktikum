# Docker Compose

## Docker Compose Commands

```bash
docker-compose --version # Check Docker Compose version
docker-compose up # Create and start containers

# List commands
docker-compose ps # List all services
docker-compose images # List all images

# Build and run commands
docker-compose build # Build or rebuild services
docker-compose up -d # Create and start containers in detached mode
docker-compose down # Stop and remove containers, networks, images, and volumes

# Exec commands in a running container
docker-compose exec <service-name> <command> # Execute a command in a running container
```

## Project Structure and Example

```
my-project/
    backend/
        Dockerfile
        package.json
        server.js
    frontend/
        Dockerfile
        package.json
        index.html
    docker-compose.yml
```

**docker-compose.yaml**:

```yaml
version: "3.8" # Version of the Compose file format

services: # Define the services that make up the app
  my-backend-service: # Service name
    image: my-backend-image:latest # Specifies the image to use (avoids <none> images in the Docker Desktop UI)
    build: ./backend # Specifies the build context (Dockerfile location)
    ports:
      - "3030:3000" # Maps the "internal" port 3000 to the "external" port 3030
    environment:
      - ENVVAR_1=value1
    depends_on:
      - my-database-service

  my-frontend-service:
    image: my-frontend-image:latest
    build: ./frontend
    ports:
      - "8080:80"
    environment:
      - ENVVAR_2=value2
    depends_on:
      - my-backend-service

  my-database-service:
    image: postgres:latest # Pulls the latest PostgreSQL image from Docker Hub
    env_file: .env
    command: postgres -c max_connections=200
```

The `docker-compose.yml` file defines the services that make up the app.
In this example, there are three services: `my-backend-service`, `my-frontend-service`, and `my-database-service`.
