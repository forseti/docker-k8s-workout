# 02_docker_client

#### Basic Commands
##### Run a container
```bash
docker run <container_image>
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
docker stop <container_id>
````

##### Kill a container
````bash
docker kill <container_id>
````

##### Remove unused resources
````bash
docker system prune
````

##### Go into a container through shell
```bash
docker exec -it <container_id> sh
```

##### Start a container with shell
```bash
docker run -it <container_image> sh
docker run -it redis sh
```