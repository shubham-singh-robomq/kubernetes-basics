# Pods

Pods are the smallest deployable units in Kubernetes. They represent a single instance of a running process in your cluster.

## What is a Pod?

A Pod is a group of one or more containers that:
- Share the same network namespace
- Share the same storage volumes
- Are scheduled together on the same node
- Share the same lifecycle

## Pod Characteristics

### 1. Shared Resources
- Network: Containers in a Pod share the same IP address and port space
- Storage: Volumes are shared between containers
- IPC: Containers can communicate using inter-process communication

### 2. Lifecycle
- Created
- Running
- Succeeded/Failed
- Deleted

## Pod Types

### 1. Single Container Pods
Most common type, running a single container:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```

### 2. Multi-Container Pods
Containers that work together:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-app
spec:
  containers:
  - name: web
    image: nginx
  - name: log-collector
    image: fluentd
```

## Common Use Cases

### 1. Sidecar Containers
- Log collection
- Monitoring
- Data synchronization

### 2. Adapter Containers
- Data format conversion
- Protocol translation

### 3. Ambassador Containers
- Proxy connections
- Service discovery

## Pod Management

### 1. Creating Pods
```bash
kubectl create -f pod.yaml
kubectl run nginx --image=nginx
```

### 2. Viewing Pods
```bash
kubectl get pods
kubectl describe pod <pod-name>
```

### 3. Deleting Pods
```bash
kubectl delete pod <pod-name>
```

## Pod Configuration

### 1. Resource Limits
```yaml
spec:
  containers:
  - name: nginx
    resources:
      limits:
        cpu: "1"
        memory: "512Mi"
      requests:
        cpu: "0.5"
        memory: "256Mi"
```

### 2. Environment Variables
```yaml
spec:
  containers:
  - name: nginx
    env:
    - name: ENV_VAR
      value: "value"
```

### 3. Volume Mounts
```yaml
spec:
  containers:
  - name: nginx
    volumeMounts:
    - name: shared-data
      mountPath: /data
  volumes:
  - name: shared-data
    emptyDir: {}
```

## Best Practices

1. **One Process per Container**
   - Keep containers focused
   - Easier to scale
   - Better isolation

2. **Resource Management**
   - Set resource limits
   - Define resource requests
   - Monitor usage

3. **Health Checks**
   - Use liveness probes
   - Implement readiness probes
   - Configure startup probes

4. **Security**
   - Run as non-root
   - Use security contexts
   - Implement network policies

## Next Steps

Learn about [Deployments](deployments.md) to manage your Pods effectively in production environments. 