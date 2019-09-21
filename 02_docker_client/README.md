# 02_docker_client

#### Basic Commands
##### Run a container
```bash
docker run <DOCKER_IMAGE_TAG>
docker run redis
```

##### List running containers
````bash
docker ps
````

##### List all containers (both running and inactive ones)
````bash
docker ps --all
````

##### Stop a container
````bash
docker stop <CONTAINER_ID>
````

##### Kill a container
````bash
docker kill <CONTAINER_ID>
````

##### Remove unused resources
````bash
docker system prune
````

##### Go into a container through shell
```bash
docker exec -it <CONTAINER_ID> sh
```

##### Start a container with shell
```bash
docker run -it <DOCKER_IMAGE_TAG> sh
docker run -it redis sh
```