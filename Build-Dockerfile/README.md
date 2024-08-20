# Dockerfile and Builder Pattern

## Overview

A Dockerfile is a script containing a series of commands used to build a Docker image. The builder pattern in Docker, particularly using multi-stage builds, optimizes and streamlines the creation of Docker images by separating the build environment from the runtime environment. This technique results in smaller, more efficient images that only include the necessary runtime dependencies.

## Builder Main Commands

### Command Descriptions

Here’s a list of essential Dockerfile commands used in building Docker images:

| Command           | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| **FROM**          | Specifies the base image for the build. This is the starting point for the image. |
| **MAINTAINER**    | Adds metadata with the name and email of the maintainer.                     |
| **COPY**          | Copies files from the context into the container at the specified location.  |
| **ADD**           | Similar to `COPY` but can also extract tar files and accept URLs.            |
| **RUN**           | Executes a command inside the container during the build process.            |
| **USER**          | Sets the default username for running subsequent commands.                   |
| **WORKDIR**       | Sets the default working directory for subsequent commands.                  |
| **CMD**           | Specifies the default command to run when a container is started.            |
| **ENV**           | Sets environment variables inside the container.                             |

## Builder Pattern in Docker

The builder pattern in Docker uses a multi-stage build process, where one stage is used for building the application, and another stage is used for packaging the application for runtime. This pattern helps to reduce the size of the final Docker image by excluding unnecessary build dependencies from the runtime environment.

### Key Commands in the Builder Pattern

- **FROM**: Defines the base image for each stage of the build.
  ```Dockerfile
  FROM base_image_for_building AS build_stage
  ```
- **RUN**: Executes commands to install dependencies and build the application.
  ```Dockerfile
  RUN apt-get update && apt-get install -y build-essential
  RUN npm install
  RUN go build -o my_app
  ```
- **COPY/ADD**: Copies files from the local directory into the container.
  ```Dockerfile
  COPY . /app
  ```
- **WORKDIR**: Sets the working directory inside the container.
  ```Dockerfile
  WORKDIR /app
  ```
- **FROM (second stage)**: Starts a new stage for the runtime environment.
  ```Dockerfile
  FROM base_image_for_runtime AS runtime_stage
  ```
- **COPY --from**: Copies files from the build stage to the runtime stage.
  ```Dockerfile
  COPY --from=build_stage /app/my_app /app/my_app
  ```
- **CMD/ENTRYPOINT**: Specifies the command or entry point to run when the container starts.
  ```Dockerfile
  CMD ["/app/my_app"]
  ```

### Example Multi-Stage Dockerfile

Here’s an example of a multi-stage Dockerfile using the builder pattern:

```Dockerfile
# Build stage
FROM golang:1.16 AS build_stage
WORKDIR /app
COPY . .
RUN go build -o my_app

# Runtime stage
FROM alpine:latest AS runtime_stage
WORKDIR /app
COPY --from=build_stage /app/my_app /app/my_app
CMD ["/app/my_app"]
```

This Dockerfile builds the application in the first stage and then creates a smaller runtime image that only includes the necessary binary.

## Docker CLI Commands

The Docker CLI (Command Line Interface) provides powerful commands for building and managing Docker images and containers. Below are some essential commands related to image and container operations:

### Docker Build

```bash
docker build [options] -t "app/container_name" .
```
- This command creates a Docker image from a Dockerfile.
- The `-t` option assigns a tag or name to the built image.
- The `.` specifies the build context, usually the directory where the Dockerfile is located.

### Docker Run

```bash
docker run [options] IMAGE
```
- This command runs a command or application in a new Docker container based on the specified image.
- The `IMAGE` parameter is the name or ID of the image you want to run.