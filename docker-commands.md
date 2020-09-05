# Show docker version
docker -v

# Show docker info
docker info

# List images
docker images || docker image ls

# List Containers running
docker ps

# List all Containers
docker ps -a

# Search for a image
docker search image_name

# Stop a Container
docker stop container_id

# Remove a Container
docker rm container_id

# Remove a Image
docker image rm image_id

# Start a Container
docker start container_name || docker start container_id

# Excecute commands inside the container
docker exec -it container_id [bash]

# Create a PostgreSQL Container
docker run --name postgres-test -e POSTGRES_PASSWORD=docker -e POSTGRES_USER=docker -p 5000:5432 -d postgres

# Show Container Logs
docker logs container_name

# Show Container Status
docker stats container_name