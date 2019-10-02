# 12_kubernetes
#### Docker Desktop's Kubernetes
##### Troubleshooting "Kubernetes is starting..."
Open the PowerShell and run the following command to set the `KUBECONFIG` variable environment to `$HOME\.kube\config`. The solutions is copied from [here](https://github.com/docker/for-win/issues/1649#issuecomment-366658253)
```powershell
[Environment]::SetEnvironmentVariable("KUBECONFIG", $HOME + "\.kube\config", [EnvironmentVariableTarget]::Machine)
```
##### kubectl #####
`kubectl` is a CLI tool that we can use to communicate with Kubernetes' master. The master has many roles, for example to manage Kubernetes' nodes (e.g. networking, load balancing, etc).

To list Kubernetes' cluster info
```console
kubectl cluster-info
kubectl cluster-info dump
```

To apply the configuration file
```console
kubectl apply -f <FILENAME>
kubectl apply -f client-pod.yml
kubectl apply -f client-node-port.yml
```

To list Kubernetes' objects
```console
kubectl get <KIND>
kubectl get pods
kubectl get services
```