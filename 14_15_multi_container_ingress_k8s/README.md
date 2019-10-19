# 14_multi_container_ingress_k8s

#### Objects

| Object Types | Description |
|---|---|
| Pods | Runs one or more closely related containers |
| Services | Sets up networking in a Kubernetes cluster |
| Secrets | Securely stores a piece of information in the cluster, such as a database password |

#### Services

| Service Types | Description |
|---|---|
| ClusterIP | Exposes a set of pods to other objects in the cluster |
| NodePort | Exposes a set of pods to the outside world (only good for dev purposes) |
| LoadBalancer | Legacy way of getting network traffic into a cluster |
| Ingress | Expose a set of services to the outside world |

#### Combined Configuration

We can have a combined configurations in `.yml` files. All we need is to have a separator `---` between each configurations. For example, if we want to combine two `ClusterIP` services:
``` yaml
apiVersion: v1
kind: Service
metadata:
  name: api-cluster-ip
spec:
  type: ClusterIP
  selector:
    component: server
  ports:
    - port: 5000
      targetPort: 5000
---
apiVersion: v1
kind: Service
metadata:
  name: client-cluster-ip
spec:
  type: ClusterIP
  selector:
    component: web
  ports:
    - port: 3000
      targetPort: 3000
```

#### Storage

Storage is used by Kubernetes to store data. There are two types of Storage: Volume and Persistent Volume.

##### Volume

Volume exists inside a Pod. If the Pod is destroyed, so is the Volume.

##### Persistent Volume (PV) and Persistent Volume Claim (PVC)

PV exists outside a Pod. It will continue to exist even if the Pod is destroyed. PVC is a request for Kubernetes to create a PV.

There are two types of PV:

| PV Type | Description |
|---|---|
| Statically Provisioned PV | Persistent Volume that is created ahead of time |
| Dynamic Provisioned PV | Persistent Volume that is created on the fly |

There are three access modes for PVC:

| Access Mode | Description |
|---|---|
| ReadWriteOnce | Can be used by a single node |
| ReadOnlyMany | Multiple nodes can read from this |
| ReadWriteMany | Can be read and written to by many nodes |

The available storage classes can be found at: https://kubernetes.io/docs/concepts/storage/storage-classes/

#### Secret

To store sensitive data, we create a secret using `kubectl`:
```console
kubectl create secret <SECRET_TYPE> <SECRET_NAME> --from-literal <KEY>=<VALUE>
```

`<SECRET_TYPE>` can be `docker-registry`, `generic`, etc

For example:
```console
kubectl create secret generic pg-password --from-literal PG_PASSWORD=12345asdf 
```

#### Ingress ([`ingress-nginx`](https://github.com/kubernetes/ingress-nginx))

Ingress Controller governs and routes the incoming traffic, and also watches for changes to the ingress.
Ingress Config is an object that has a set of rules describing how traffic should be routed.

##### Installation

For Docker Desktop, first run **Mandatory Command**:
```console
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml
```

Then enable the service, using the following command:
```console
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml
```

To verify the Ingress service is enabled:
```console
kubectl get svc -n ingress-nginx
```

##### Debugging/Troubleshooting

First, check if the endpoints are up:
```console
kubectl get endpoints
```

If one of them has no endpoints, check the pods to get the `<POD_NAME>`:
```console
kubectl get pods
```

Then run the following command to see the errors:
```console
kubectl describe pods <POD_NAME>
```

#### Dashboard

To setup Dashboard for local development (with Git Bash), download the `kubernetes-dashboard.yaml`:
```console
curl -O https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
```

Edit the file. At `line 116`, add below `--auto-generate-certificates`:
```yaml
args:
  - --auto-generate-certificates
  - --enable-skip-login
  - --disable-settings-authorizer
```

Then apply the changes:
```console
kubectl apply -f kubernetes-dashboard.yaml
```

Start the server:
```console
kubectl proxy
```

Go to the browser and enter URL: `http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/`

You will be presented with the login screen, so click `SKIP`.

**Warning:** Do not do this when deploying kubernetes clusters to a public facing server!

#### Running the Demo
If You're using Docker Desktop, sometimes Kubernetes may hang. So restart the cluster using the Docker Desktop Settings.

Once it's up, do the following commands in order:
1. `kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml`
2. `kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml`
3. `kubectl create secret generic pg-password --from-literal PG_PASSWORD=pgpassword123`
4. `kubectl apply -f k8s`