# 03_redis_image
Two ways:
1. Dockerfile
2. Manual Commit

#### Create Image (Dockerfile)
##### Create Dockerfile
```docker
FROM alpine

RUN apk add --update redis

CMD ["redis-server"]
```

##### Build the image
```bash
docker build .
```

##### Run our new image
```
docker run <DOCKER_IMAGE_ID>
```

##### Build the image (Using tag)
```bash
docker build -t <DOCKERHUB_USERNAME>/<TAG> .
docker build -t yourusername/redis .
```
Note that `<DOCKERHUB_USERNAME>/<TAG>` combination forms a `<DOCKER_IMAGE_TAG>` for our image.

##### Run our new image
```
docker run <DOCKER_IMAGE_TAG>
docker run yourusername/redis
```

#### Create Image (Manual Commit)

##### Start 'alpine' with a shell
```bash
docker run -it alpine sh
```

##### Inside 'alpine' (/#)
```bash
apk add --update redis
```

##### Commit
```bash
docker commit -c 'CMD ["redis-server"]' <CONTAINER_ID>
```