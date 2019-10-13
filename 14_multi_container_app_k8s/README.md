# 14_multi_container_apps_k8s

## General 
| Object Types | Description |
|---|---|
| Pods | Runs one or more closely related containers |
| Services | Sets up networking in a Kubernetes cluster |

#### Services

| Service Types | Description |
|---|---|
| ClusterIP | Exposes a set of pods to other objects in the cluster |
| NodePort | Exposes a set of pods to the outside world (only good for dev purposes) |

##### Combined Configuration

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