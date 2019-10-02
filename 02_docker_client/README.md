# 02_docker_client

#### Basic Commands
##### Run a container
```console
docker run <DOCKER_IMAGE_TAG>
docker run redis
```

##### List running containers
````console
docker ps
````

##### List all containers (both running and inactive ones)
````console
docker ps --all
````

##### Stop a container
````console
docker stop <CONTAINER_ID>
````

##### Kill a container
````console
docker kill <CONTAINER_ID>
````

##### Remove unused resources
````console
docker system prune
````

##### Go into a container through shell
```console
docker exec -it <CONTAINER_ID> sh
```

##### Start a container with shell
```console
docker run -it <DOCKER_IMAGE_TAG> sh
docker run -it redis sh
```