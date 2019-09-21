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

##### Build image
```bash
docker build .
```

##### Build image (Using tag)
```bash
docker build . -t <dockerhub_username>/<tag>:latest
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
docker commit -c 'CMD ["redis-server"]' <container_id>
```