# Docker Container Inspection

Inspecting Docker containers is crucial for troubleshooting and understanding the state of your containers. Docker provides several commands to inspect and gather information about your containers. Below are some essential commands and their descriptions:

### List Running Containers

- **`docker ps`**: Lists all running containers.

  ```bash
  docker ps
  ```

### List All Containers

- **`docker ps -a`**: Lists all containers, including those that are stopped.

  ```bash
  docker ps -a
  ```

### View Container Logs

- **`docker logs [-f] container`**: Shows the output (stdout and stderr) from the container. The `-f` flag allows you to follow the log output.

  ```bash
  docker logs my_container_name
  docker logs -f my_container_name
  ```

### Show Differences with the Image

- **`docker diff container`**: Shows the differences between the container's filesystem and the base image. This command displays files that have been added, deleted, or modified.

  ```bash
  docker diff my_container_name
  ```

### Display Running Processes

- **`docker top container`**: Displays the running processes inside a container.

  ```bash
  docker top my_container_name
  ```

### Inspect Container Details

- **`docker inspect [OPTIONS] container`**: Provides detailed information about a container. You can use the `--format` option to extract specific information from the JSON output.

  ```bash
  docker inspect my_container_name
  ```

  *Example: Extracting the image used by the container:*

  ```bash
  docker inspect --format='{{ .Config.Image }}' my_container_name
  ```

These commands allow you to gain insights into the state, logs, and configuration of your Docker containers. Use them to manage and troubleshoot your containers effectively.