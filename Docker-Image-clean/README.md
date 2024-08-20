# Docker Clean

Cleaning up your Docker environment is essential to free up disk space and ensure efficient resource usage. Below are some commands to help you manage and prune unused Docker resources.

## Prune Unused Images
To clean or prune unused (dangling) images:
```bash
docker image prune
```

## Remove All Unused Images
To remove all images that are not associated with any running containers (including dangling images):
```bash
docker image prune -a
```

## Prune Entire System
To clean up your entire Docker system, including unused images, containers, networks, and volumes:
```bash
docker system prune
```

## Leave a Docker Swarm
If your Docker instance is part of a swarm, you can leave the swarm with:
```bash
docker swarm leave
```

## Remove a Docker Stack
To remove a Docker stack (including all associated services and volumes) from a swarm cluster:
```bash
docker stack rm STACK_NAME
```

## Kill All Running Containers
To kill all currently running Docker containers:
```bash
docker kill $(docker ps -q)
```

### Important Notes
- **docker swarm leave** should be executed on a worker or manager node within the swarm.
- **docker stack rm** is used to remove a Docker stack from a swarm cluster.
- Use **docker system prune** with caution, as it removes all unused data and cannot be undone. Always review the list of items to be pruned before confirming the action.