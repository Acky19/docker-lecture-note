# Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services, networks, and volumes. You can then create and start all the services from your configuration with a single command.

## Basic Example

Here's a basic example of a `docker-compose.yml` file:

```yaml
version: '3'
services:
  web:
    build: .
    # build from Dockerfile
    context: ./Path
    dockerfile: Dockerfile
    ports:
      - "5000:5000"
    volumes:
      - .:/code
  redis:
    image: redis
```

## Example: Nginx Setup

Here's an example of a `docker-compose.yml` file for setting up Nginx with a static website:

```yaml
version: '3'
services:
  nginx:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    networks:
      - webnet

networks:
  webnet:
    driver: bridge
```

In this example:

- The `nginx` service uses the latest Nginx image from Docker Hub.
- It maps port 8080 on the host to port 80 on the container, allowing you to access the Nginx server via `http://localhost:8080`.
- It mounts a local directory `./html` to `/usr/share/nginx/html` in the container, which is where Nginx serves static files from.
- It connects to a custom network `webnet`.

Make sure you have an `html` directory with your static files (e.g., `index.html`) in the same directory as your `docker-compose.yml`.

## Commands

Below is a list of commonly used Docker Compose commands:

- **`docker compose start`**: Starts existing containers for a service.

  ```bash
  docker compose start
  ```

- **`docker compose stop`**: Stops running containers without removing them.

  ```bash
  docker compose stop
  ```

- **`docker compose pause`**: Pauses running containers.

  ```bash
  docker compose pause
  ```

- **`docker compose unpause`**: Unpauses paused containers.

  ```bash
  docker compose unpause
  ```

- **`docker compose ps`**: Lists the containers.

  ```bash
  docker compose ps
  ```

- **`docker compose up`**: Builds, (re)creates, starts, and attaches to containers for a service.

  ```bash
  docker compose up
  ```

- **`docker compose down`**: Stops and removes containers, networks, volumes, and images created by `docker compose up`.

  ```bash
  docker compose down
  ```

## Reference

### Building

- **Basic build configuration:**

  ```yaml
  web:
    build: .
  ```

- **Build from custom Dockerfile:**

  ```yaml
  build:
    context: ./dir
    dockerfile: Dockerfile.dev
  ```

- **Build from an image:**

  ```yaml
  image: ubuntu
  image: ubuntu:14.04
  image: tutum/influxdb
  image: example-registry:4000/postgresql
  image: a4bc65fd
  ```

### Ports

- **Expose ports:**

  ```yaml
  ports:
    - "3000"
    - "8000:80" # guest:host
  ```

- **Expose ports to linked services (not to host):**

  ```yaml
  expose: ["3000"]
  ```

### Commands

- **Command to execute:**

  ```yaml
  command: bundle exec thin -p 3000
  command: [bundle, exec, thin, -p, 3000]
  ```

- **Override the entrypoint:**

  ```yaml
  entrypoint: /app/start.sh
  entrypoint: [php, -d, vendor/bin/phpunit]
  ```

### Environment Variables

- **Environment variables:**

  ```yaml
  environment:
    RACK_ENV: development
  environment:
    - RACK_ENV=development
  ```

- **Environment variables from a file:**

  ```yaml
  env_file: .env
  env_file: [.env, .development.env]
  ```

### Dependencies

- **Link services:**

  ```yaml
  links:
    - db:database
    - redis
  ```

- **Ensure service availability:**

  ```yaml
  depends_on:
    - db
  ```

For more detailed information, refer to the [Docker Compose documentation](https://docs.docker.com/compose/).

---