
# Docker Networking Tutorial

## Prerequisites

Before proceeding with the tutorial, ensure that Docker and Docker Compose are installed on your Ubuntu system. You can follow the installation instructions from the official Docker documentation:

- [Install Docker on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

## Networking in Docker

### Instructions

1. **Display all existing networks in the host:**
   ```bash
   docker network ls
   ```

2. **Create a new bridge network:**
   ```bash
   docker network create -d bridge my-bridge-network
   ```

3. **Run a container linked to the created network:**
   ```bash
   docker run -d -p 8081:8081 -e "port=8081" --name app --network=my-bridge-network selaworkshops/python-app:2.0
   ```

4. **Find the container's internal IP using:**
   ```bash
   docker inspect app
   ```
   - Look for the `IPAddress` under `"my-bridge-network"`.

5. **Open a new terminal window and run an Alpine container in interactive mode:**
   ```bash
   docker run -it --name client alpine:latest
   ```

6. **Install `curl` in the client container:**
   ```bash
   apk --no-cache add curl  
   ```

7. **From the client container terminal, try to browse to the app container (replace the IP Address accordingly):**
   ```bash
   curl 172.21.0.2:8081 --connect-timeout 5
   ```
   - You should get a timeout error because the containers are not yet connected via the bridge network.

8. **Attach the client container to the created network:**
   ```bash
   docker network connect my-bridge-network client
   ```

9. **Browse to the app container again from the client container terminal:**
   ```bash
   curl 172.21.0.2:8081 --connect-timeout 5
   ```
   - You should now see the output: `<h1>Python App</h1>`

10. **Inspect the network from the regular terminal and look for the linked containers:**
    ```bash
    docker inspect my-bridge-network
    ```

11. **Disconnect both containers from the created network:**
    ```bash
    docker network disconnect my-bridge-network app
    docker network disconnect my-bridge-network client
    ```

12. **Delete the network:**
    ```bash
    docker network rm my-bridge-network
    ```

13. **Ensure that the network was deleted:**
    ```bash
    docker network ls
    ```

14. **Exit from the client container and close the terminal:**
    ```bash
    exit
    exit
    ```