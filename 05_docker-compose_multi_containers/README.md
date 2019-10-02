
# 05_docker_compose_multi_containers

This project is an example of running a multi-tier application that use Node.js for the web application and Redis as the datastore.

#### Docker Compose (Basics)
For this section use `0501_visits_app` sub-project.

##### Run our multi-tier application
```console
docker-compose up
```

##### Build before running our multi-tier application
```console
docker-compose up --build
```

##### Run our multi-tier application as daemon process
```console
docker-compose up -d
```

##### Terminate our multi-tier application
```console
docker-compose down
```

##### Check the process
```console
docker-compose ps
```

#### Restart Policies
For this section, use the following sub-projects
1. `0502_visits_app_restart_always`
2. `0503_visits_app_restart_on-failure`

Specify restart policy under the targeted container.

```yaml
services:
  node-app:
    restart: always
```

|	Policy		 |	Description														 |
|----------------|-------------------------------------------------------------------|
| "no" 			 | Never attempts to restart this container if it stops or crashes   |
| always		 | If this container stops "for any reason" always try to restart it |
| on-failure	 | Only restart if the container stops with an error code (> 0) 	 |
| unless-stopped | Always restart unless we (the developers) forcibly stop it 		 |

`always` works best for web applications.

`on-failure` works best for workers.

Note that `"no"` has double quotes. This is because YAML will treat `no` as boolean value, therefore the quotes are required.

```yaml
services:
  node-app:
    restart: "no"
```