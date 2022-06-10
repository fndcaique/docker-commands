# Show docker version
- docker -v

# Show docker info
- docker info

# List images
- docker images
- docker image ls

# Search for a image
- docker search image_name

# Remove a image
- docker image rm image_id

# Create a container
- docker [container] create <params> <image>:<tag>
- docker [container] create -it <image>:<tag>

# Create and run a container
- docker [container] run <params> <image>:<tag>

## Cleanup mode
- docker [container] run --rm <image>:<tag>

## Run in background (--detach)
- docker [container] run -d <image>:<tag>

## Run back in the foreground (attach)
- docker [container] attach <container_id || container_name>

# Create a PostgreSQL container
- docker run --name postgres-test -e POSTGRES_PASSWORD=docker -e POSTGRES_USER=docker -p 5000:5432 -d postgres

# List containers running
- docker ps
- docker container ls

# List all containers
- docker ps -a
- docker container ls -a

# List the last container
- docker ps -l
- docker container ls -l  

# Start a container
- docker [container] start <container_name || container_id>

# Restart a container
- docker [container] restart <container_id || container_name>

# Pause a container
- docker [container] pause <container_id || container_name>

# Unpause a container
- docker [container] unpause <container_id || container_name>

# Stop a container
- docker stop container_id

# Execute commands inside the container
- docker exec -it container_id [bash]

# Show container Logs
- docker logs container_name

# Show container Status
- docker stats container_name

# Remove a container
- docker [conatiner] rm [-f] <container_id || container_name>

# Remove all stopped containers ! :warning: !
- docker container prune

# Monitoring a container
docker [container] top <container_id || container_name>
