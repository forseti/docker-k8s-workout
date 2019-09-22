# 06_production_workflow

#### Initial Setup
##### Windows 10 (Git Bash)

```bash
echo "export MSYS_NO_PATHCONV=1" >> ~/.bash_profile
```

#### Build and Run Application
##### Build our image
```bash
docker build -f Dockerfile.dev -t <DOCKERHUB_USERNAME>/<TAG> .
docker build -f Dockerfile.dev -t yourusername/frontend .
```

##### Run our image as a container
```bash
docker run -p 3000:3000 -v /opt/frontend/node_modules -v $(pwd):/opt/frontend <DOCKER_IMAGE_TAG> .
docker run -p 3000:3000 -v /opt/frontend/node_modules -v $(pwd):/opt/frontend yourusername/frontend .
```
Note that the `-v /opt/frontend/node_modules` excludes the folder `/opt/frontend/node_modules` in the container from being mapped in the following `-v $(pwd)/opt/frontend` mounting (or any subsequent `-v` mountings).

##### Run test on our container
```bash

docker run -it <CONTAINER_ID> npm run test
```

##### Run test on our container with `docker-compose`
Run the `docker-compose`
```bash
docker-compose up
```

##### Run interactive test through `docker` client
Get the `<CONTAINER_ID>` of `web` from `docker-compose` session using `docker ps`
```bash
docker ps
```

Use `docker exec` to run `npm run test`
```bash
docker exec -it <CONTAINER_ID> npm run test
```