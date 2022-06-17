# Docker

## Show docker version

- docker -v

## Show docker info

- docker info

## Docker images

### List images

- docker images
- docker image ls

### Search for a image

- docker search <image_name>

## Download a image

- docker pull <image_name>

### Remove a image

- docker image rm <image_id>
- docker rmi [-f] <image_id>

## Docker containers

### Create a container

- docker [container] create <container_params> <image_name>:<image_tag>
- docker [container] create -it <image_name>:<image_tag>

### Create and run a container

- docker [container] run <container_params> <image_name>:<image_tag>

#### Cleanup mode

- docker [container] run --rm <image_name>:<image_tag>

#### Run in background (--detach)

- docker [container] run -d <image_name>:<image_tag>

#### Run back in the foreground (attach)

- docker [container] attach <container_id || container_name>

### Create a PostgreSQL container

- docker run --name postgres-test -e POSTGRES_PASSWORD=docker -e POSTGRES_USER=docker -p 5000:5432 -d postgres

### List containers running

- docker ps
- docker container ls

### List all containers

- docker ps -a
- docker container ls -a

### List the last container

- docker ps -l
- docker container ls -l  

### Start a container | Iniciar um container

- docker [container] start [-ai] <container_name || container_id>

> `-ai` a = attach, i = interactive

### Restart a container | Reiniciar um container

- docker [container] restart <container_id || container_name>

### Pause a container | Pausar um container

- docker [container] pause <container_id || container_name>

### Unpause a container | Despausar um container

- docker [container] unpause <container_id || container_name>

### Stop a container | Parar um container

- docker stop container_id

### Execute commands inside the container | Executar comandos dentro do container

- docker exec -it <container_id> [bash]

### Show container Logs | Exibir os logs do container

- docker logs <container_name>

### Show container Status | Exibir o status do container

- docker stats <container_name>

### Inspect a container | Inspecionar um container

docker inspect <container_name>

### Remove a container | Remover um container

- docker [conatiner] rm [-f] <container_id || container_name>

### Remove all stopped containers ! :warning

- docker container prune

### Monitoring a container

docker [container] top <container_id || container_name>

## Dockerfile

`FROM` Utilizado para definir a imagem base

Exemplo:

- `FROM ubuntu:latest [AS alias-de-sua-preferencia]`

`WORKDIR` Utilizado para definir o diretório base em que serão executados os comandos

Exemplo:

- `WORKDIR /caminho/para/o/diretorio`

`COPY` Utilizado para copiar arquivos e/ou diretórios

Exemplo:

- `COPY file1 file2 fileN target_dir`
- `COPY ["file1", "file2", "fileN", "target_dir"]`

`RUN` Utilizado para executar comandos durante a criação da imagem docker

Exemplo:

- `RUN npm run build`

`EXPOSE` Utilizado para expor a porta em que a aplicação irá rodar

Exemplo

- `EXPOSE 5000`

`CMD`

`ENTRYPOINT`

`LABEL`

`ENV`

`USER`

`VOLUME`

### Building a image

`docker image build [it <image_name:image_tag>] <dockerfile_directory>`

### Layers and Cache

## Network

`docker network ls` Utilizado para listar as redes existentes no docker. Por padrão ele possui 3 (bridge, host e none)

### Bridge

Rede default de associação dos containers
Todos os containers associados a essa rede podem se comunicar via TCP/IP

### Host

Containers associados a essa rede compartilham de toda a rede da máquina que executa o ambiente Docker

### None

Containers associados a essa rede ficam isolados. ütil para containers que utilizam arquivos para a execução de comandos e/ou comunicação

### Your network

#### Create a network

`docker network create -d bridge <network-name>`

#### Connect network with created container

`docker network connect <network-name> <container_name>`

#### Disconnect container from a network

`docker network disconnect <network_name> <container_name>`

## Volumes

### Rodar container vinculando um volume

docker run -d --name <container_name> -p 8881:80 -v "/path/dir/:/usr/local/apache2/htdocs/" httpd:2.4

### Listar volumes

docker volume ls

### Remover um volume

docker volume rm <volume_name>

### Remover todos os volumes não utilizados no momento

docker volume prune

### Remover um container e o seu volume

docker [container] rm -v <container_id> || <container_name>

## Docker Compose

- docker-compose.yaml

```yaml
version: "<compose_version>"
services: # Definition of services/containers
  <service_1_name>:
    image: <image_name:tag> # example with a build
    # some configs...
  <service_2_name>:
    build: <dockerfile_path> # example with a `Dockerfile`
    volumes:
      - type: volume
        source: mydata
        target: /data
        volume:
          nocopy: true
      - type: bind
        source: ./static
        target: /opt/app/static
    networks:
      - network_1
  <service_N_name>:
    image: <image_name:tag>
    restart: always # no|on-failure|always|unless-stopped # The default value is no
    ports:
      - 3567:3000
    environment:
      - DB_HOST:localhost
    depends_on:
      - "service_1_name"
    volumes:
      - "/var/run/postgres/postgres.sock:/var/run/postgres/postgres.sock"
      - "dbdata:/var/lib/postgresql/data"
    networks:
      - network_1
      - network_2
volumes:
  mydata:
  dbdata:
networks:
  network_1:
  network_2:
        
```

`docker-compose up [--build [<service_name>]]` Utilizado para executar todos os services/containers

`docker-compose up [--build] <service_name>` Utilizado para especificar qual service queremos executar (suas dependencias também serão executadas)

`docker-compose down` Utilizado para parar os serviços e remover objetos criados

`docker-compose ps` Utilizado para listar os containers pertencentes ao arquivo compose

`docker-compose stop [<service_name>]` Utilizado para parar os serviços

`docker-compose start [<service_name>]`

`docker-compose logs -f --tail=100 [<service_name>]`
