# Docker Container Management

Managing Docker containers is essential for working effectively with Docker. Below are some of the most commonly used commands for managing containers:

### List Running Containers

- **`docker ps`**: Lists all running containers on your system.

  ```bash
  docker ps
  ```

### List All Containers

- **`docker ps -a`**: Lists all containers, including those that are stopped.

  ```bash
  docker ps -a
  ```

### Start Containers

- **`docker start`**: Starts one or more stopped containers.

  ```bash
  docker start <container_name_or_id>
  ```

### Stop Containers

- **`docker stop`**: Stops one or more running containers.

  ```bash
  docker stop <container_name_or_id>
  ```

### Restart Containers

- **`docker restart`**: Stops and then starts a container.

  ```bash
  docker restart <container_name_or_id>
  ```

### Remove Containers

- **`docker rm`**: Removes one or more containers. Use this command with caution, as it permanently deletes the containers.

  ```bash
  docker rm <container_name_or_id>
  ```

These commands are the foundation of managing Docker containers, allowing you to list, start, stop, restart, and remove containers as needed.