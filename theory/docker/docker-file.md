# Dockerfile

A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.
Using `docker build`, users can create an automated build that executes several command-line instructions in succession.

## Example Dockerfile

```dockerfile
# Use an official Python runtime as the base image
FROM python:3.7-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install requirements.txt

CMD ["python", "app.py"]
```

### Commands

- `FROM`: Specifies the base image to use for the build.
- `WORKDIR`: Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow it in the Dockerfile.
- `COPY`: Copies files from the host system to the container.
- `RUN`: Executes a command in the container.
- `CMD`: Provides a command to run when the container starts.
- `ENTRYPOINT`: Provides a command to run when the container starts, and it cannot be overridden at runtime.

### Best Practices

#### Practice 1

Use official images as the base image with a specific version tag for the base image.

Images based on full OS distributions are often large and contain unnecessary packages - and often have security vulnerabilities.
`Alpine` images are smaller and more secure and are a good choice for production images.

**Example Python (https://hub.docker.com/_/python/tags):**
The `python:3.9.20-bullseye` image is based on Debian Bullseye and Python 3.9.20.
It is over 300 MB large with almost 200 possible vulnerabilities.
The `python:3.9.20-alpine3.14` image is based on Alpine 3.14 and Python 3.9.20.
It is only 50 MB large with less than 10 possible vulnerabilities.

#### Practice 2

Optimize Caching Image Layers.

Each command in a Dockerfile creates a new layer in the image.
Images also already have layers from the base image.
Example:

```dockerfile
FROM python:3.9.20-alpine3.14

WORKDIR /app
COPY myapp.py .

RUN pip install -r requirements.txt
```

This adds 4 layers to the image: the base image, the `WORKDIR` layer, the `COPY` layer, and the `RUN` layer.
If a layer changes, all following layers (so all the lines below the changed layer) have to be rebuilt.
To optimize caching, put commands that change frequently at the end of the Dockerfile.
A better version of the Dockerfile:

```dockerfile
FROM python:3.9.20-alpine3.14

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY myapp.py .
```

This way, the `COPY myapp.py .` command is only executed when the `myapp.py` file changes.
The `pip install -r requirements.txt` command is only executed when the `requirements.txt` file changes.

#### Practice 3

Use `.dockerignore` to exclude unnecessary files and directories from the build context.
This can speed up the build process and reduce the size of the final image.

#### Practice 4

Make use of Multi-Staged Builds to reduce the size of the final image.
This is especially useful when building applications that require build tools and dependencies that are not needed at runtime.

```dockerfile
# Build Stage
FROM node:14.17.6 as build

WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

# Production Stage
FROM nginx:1.21.1-alpine

COPY --from=build /app/build /usr/share/nginx/html
```

#### Practice 5

Not using root user in the container. Use a non-root user for running the application in the container.
This is a security best practice.

```dockerfile
FROM python:3.9.20-alpine3.14

...

# Create a new group called mygroup
RUN groupadd -r mygroup
# Create a new group called mygroup
RUN useradd -r -g mygroup myuser
# Set the permissions for the app directory
RUN chown -R myuser:mygroup /app
# Switch to the myuser user
USER myuser

CMD ["python", "app.py"]
```

In the Alpine-Image you might have to install `shadow` to use the `useradd` command:

```dockerfile
RUN apk add --no-cache shadow
```

##### Practice 6

Scan for vulnerabilities in the Docker image using the `docker scout` command.
This command scans the image for vulnerabilities and provides a report with the vulnerabilities found.

```bash
Usage
  docker scout [command]

Available Commands
  compare         Compare two images and display differences (experimental)
  cves            Display CVEs identified in a software artifact
  entitlement     Manage entitlement of a Docker Hub repository
  quickview       Quick overview of an image
  recommendations Display available base image updates and remediation recommendations
  stream          Record an image into a stream (experimental)
  version         Show Docker Scout version information
```

To scan for vulnerabilities in a Docker image, use the following command:

```bash
docker scout cves <image-name>
```

You can also use Snyk to scan for vulnerabilities in the Docker image:

```bash
snyk test --docker <image-name>
```
