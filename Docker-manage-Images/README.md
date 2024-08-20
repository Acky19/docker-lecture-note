# Docker Image Management

Docker images are the foundation of containers. Managing images effectively is crucial for building, sharing, and deploying applications. Below are some of the key commands used to manage Docker images:

### List Docker Images

- **`docker images`**: Lists all Docker images available on your system.

  ```bash
  docker images
  ```

### Pull Docker Images

- **`docker pull`**: Downloads Docker images from a registry (e.g., Docker Hub) to your local system.

  ```bash
  docker pull <image_name>:<tag>
  ```

  *Example:*

  ```bash
  docker pull ubuntu:latest
  ```

### Push Docker Images

- **`docker push`**: Pushes Docker images to a registry (e.g., Docker Hub) for sharing with others. Make sure you have logged into the registry before pushing.

  ```bash
  docker push <repository>/<image_name>:<tag>
  ```

  *Example:*

  ```bash
  docker push myrepo/myapp:latest
  ```

### Remove Docker Images

- **`docker rmi`**: Removes one or more Docker images from your system.

  ```bash
  docker rmi <image_name_or_id>
  ```

  *Example:*

  ```bash
  docker rmi ubuntu:latest
  ```

These commands help you manage Docker images, whether you need to list, download, upload, or delete them. Managing your images efficiently is essential for maintaining a clean and organized Docker environment.