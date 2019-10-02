# 03_build_custom_image
Two ways to build a custom image:
1. Using `Dockerfile`
2. Through a manual commit

#### Create Image (Dockerfile)
##### Create Dockerfile
```docker
FROM alpine

RUN apk add --update redis

CMD ["redis-server"]
```

##### Build the image
```console
docker build .
```

##### Run our new image
```console
docker run <DOCKER_IMAGE_ID>
```

##### Build the image (Using tag)
```console
docker build -t <DOCKERHUB_USERNAME>/<TAG> .
docker build -t yourusername/redis .
```
Note that `<DOCKERHUB_USERNAME>/<TAG>` combination forms a `<DOCKER_IMAGE_TAG>` for our image.

##### Run our new image
```console
docker run <DOCKER_IMAGE_TAG>
docker run yourusername/redis
```

#### Create Image (Manual commit)

##### Start 'alpine' with a shell
```console
docker run -it alpine sh
```

##### Inside 'alpine' (/#)
```console
apk add --update redis
```

##### Commit
```console
docker commit -c 'CMD ["redis-server"]' <CONTAINER_ID>
```