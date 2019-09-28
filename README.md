# 12_kubernetes
#### Docker Desktop's Kubernetes
##### Troubleshooting "Kubernetes is starting..."
Open the PowerShell and run the following command. The solutions is copied from [here](https://github.com/docker/for-win/issues/1649#issuecomment-366658253)
```powershell
[Environment]::SetEnvironmentVariable("KUBECONFIG", $HOME + ".kube\config", [EnvironmentVariableTarget]::Machine)
```