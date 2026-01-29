# Kubernetes Resources

## Namespace

A **Namespace** is a logical separation mechanism in Kubernetes.  
It allows you to group resources within the same cluster and apply
policies, access control, and resource limits per group.

Namespaces are *logical* because:
- All resources still run on the same physical cluster
- Kubernetes enforces isolation using rules, scope, and metadata
- Namespaces help organize environments such as `dev`, `test`, and `prod`

### Example: Create a Namespace

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

### Apply and Verify
```bash
kubectl apply -f namespaces/dev.yaml
kubectl get namespaces


NAME              STATUS   AGE
default           Active   9d
dev               Active   30s
kube-node-lease   Active   9d
kube-public       Active   9d
kube-system       Active   9d
```

## Pod
A **pod** is the smallest deployable unit in Kubernetes.

Created on dev folder a yaml file - named nginx.yaml which is a pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: demo-pod
  namespace: dev
  labels:
    app: demo
spec:
  containers:
    - name: app
      image: nginx
      ports:
        - containerPort: 80
```

Applied it with Kubectl apply -f dev/nginx.yaml (k8s/dev/nginx.yaml)

```bash
kubectl describe pod demo-pod -n dev
```
```bash
Name:             demo-pod
Namespace:        dev
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Thu, 29 Jan 2026 04:17:12 +0200
Labels:           app=demo
Annotations:      <none>
Status:           Running
IP:               10.244.0.30
IPs:
  IP:  10.244.0.30
Containers:
  app:
    Container ID:   docker://213fd16fdaf62c16e0fa79655ea666575f115c4b1ec43ff59be4fab27809f546
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:c881927c4077710ac4b1da63b83aa163937fb47457950c267d92f7e4dedf4aec
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Thu, 29 Jan 2026 04:17:15 +0200
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-kl6bw (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  kube-api-access-kl6bw:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  111s  default-scheduler  Successfully assigned dev/demo-pod to minikube
  Normal  Pulling    110s  kubelet            spec.containers{app}: Pulling image "nginx"
  Normal  Pulled     108s  kubelet            spec.containers{app}: Successfully pulled image "nginx" in 1.93s (1.93s including waiting). Image size: 160646317 bytes.
  Normal  Created    108s  kubelet            spec.containers{app}: Created container: app
  Normal  Started    108s  kubelet            spec.containers{app}: Started container app
  ```
