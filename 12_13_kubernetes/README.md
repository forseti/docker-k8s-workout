# 12_13_kubernetes
#### Docker Desktop's Kubernetes
##### Troubleshooting "Kubernetes is starting..."
Open the PowerShell and run the following command to set the `KUBECONFIG` variable environment to `$HOME\.kube\config`. The solutions is copied from [here](https://github.com/docker/for-win/issues/1649#issuecomment-366658253)
```powershell
[Environment]::SetEnvironmentVariable("KUBECONFIG", $HOME + "\.kube\config", [EnvironmentVariableTarget]::Machine)
```

##### Object's Kind #####
| Kind | Description |
|---|--------------------------------------------------------------------|
| Pods 			 | Runs one (or more closely related containers) |
| Services		 | Sets up networking in Kubernetes' Cluster |
| Deployment	 | Maintains a set of identical pods, ensuring correct configurations |

Differences between Pods and Deployment

| Pods | Deployment |
|---|---|
| Runs a single set of containers | Runs a set of identical pods (one or more) |
| Good for one-off development purposes | Monitors the state of each pod, updating as necessary |
| Rarely used in production | Good for development and production |

###### `NodePort` #######
`NodePort` exposes the service on each Node's IP at a static port. Available port's range between `30000` and `32767`

##### `kubectl` #####
`kubectl` is a CLI tool that we can use to communicate with Kubernetes' master. The master has many roles, for example to manage Kubernetes' nodes (e.g. networking, load balancing, etc).

To list Kubernetes' cluster info
```console
kubectl cluster-info
kubectl cluster-info dump
```

To apply the configuration file
```console
kubectl apply -f <CONFIG_FILENAME>
kubectl apply -f client-pod.yml
kubectl apply -f client-node-port.yml
kubectl apply -f client-deployment.yml
```

To list Kubernetes' objects (This will display <POD_NAME>, etc)
```console
kubectl get <KIND>
kubectl get pods
kubectl get services
kubectl get deployments -o wide
```

To list Kubernetes' objects (wide output)
```console
kubectl get <KIND> -o wide
kubectl get pods -o wide
kubectl get services -o wide
kubectl get deployments -o wide
```

To describe (or get detailed info about) Kubernetes' objects
```console
kubectl describe <KIND> <OBJECT_NAME>
kubectl describe pods client-pod
```

To delete Kubernetes' objects
```console
kubectl delete -f <CONFIG_FILENAME>
kubectl delete -f client-pod.yml
kubectl delete -f client-node-port.yml
```

To update images of Kubernetes' deployments
```console
kubectl set image <KIND>/<OBJECT_NAME> <CONTAINER_NAME>=<DOCKER_IMAGE_TAG>
kubectl set image deployment/client-deployment client=isometria/dkw-10-client:v1
```

To print logs of Kubernetes' pods
```console
kubectl logs <POD_NAME>
kube logs client-deployment-98f566999-fb4j6
```

To interact with Kubernetes' pods through shell
```console
kubectl exec -it <POD_NAME> bash
kubectl exec -it client-deployment-98f566999-fb4j6 bash
```