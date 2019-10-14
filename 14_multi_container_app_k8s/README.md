# 14_multi_container_apps_k8s

#### Objects

| Object Types | Description |
|---|---|
| Pods | Runs one or more closely related containers |
| Services | Sets up networking in a Kubernetes cluster |

#### Services

| Service Types | Description |
|---|---|
| ClusterIP | Exposes a set of pods to other objects in the cluster |
| NodePort | Exposes a set of pods to the outside world (only good for dev purposes) |

#### Combined Configuration

We can have a combined configurations in `.yml` files. All we need is to have a separator `---` between each configurations. For example, if we want to combine two `ClusterIP` services:
``` yaml
apiVersion: v1
kind: Service
metadata:
  name: api-cluster-ip-service
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
  name: client-cluster-ip-service
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


