# Deployments

Deployments are Kubernetes objects that manage the deployment and scaling of Pods. They provide declarative updates for Pods and ReplicaSets.

## What is a Deployment?

A Deployment:
- Manages a set of identical Pods
- Ensures a specified number of Pods are running
- Handles updates and rollbacks
- Provides scaling capabilities

## Deployment Features

### 1. Rolling Updates
- Zero-downtime deployments
- Controlled update process
- Automatic rollback on failure

### 2. Scaling
- Manual scaling
- Automatic scaling (with HPA)
- Replica management

### 3. Rollback
- Version history
- One-command rollback
- Status tracking

## Creating a Deployment

### Basic Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

## Deployment Management

### 1. Creating
```bash
kubectl create -f deployment.yaml
kubectl apply -f deployment.yaml
```

### 2. Updating
```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
kubectl edit deployment nginx-deployment
```

### 3. Scaling
```bash
kubectl scale deployment nginx-deployment --replicas=5
```

### 4. Rolling Back
```bash
kubectl rollout undo deployment/nginx-deployment
kubectl rollout undo deployment/nginx-deployment --to-revision=2
```

## Deployment Strategies

### 1. Rolling Update (Default)
```yaml
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
```

### 2. Recreate
```yaml
spec:
  strategy:
    type: Recreate
```

## Advanced Features

### 1. Probes
```yaml
spec:
  template:
    spec:
      containers:
      - name: nginx
        livenessProbe:
          httpGet:
            path: /
            port: 80
        readinessProbe:
          httpGet:
            path: /
            port: 80
```

### 2. Resource Limits
```yaml
spec:
  template:
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

### 3. Node Selection
```yaml
spec:
  template:
    spec:
      nodeSelector:
        disktype: ssd
```

## Best Practices

1. **Version Control**
   - Use version tags for images
   - Maintain deployment history
   - Document changes

2. **Resource Management**
   - Set appropriate resource limits
   - Monitor resource usage
   - Implement autoscaling

3. **Update Strategy**
   - Choose appropriate strategy
   - Set proper update parameters
   - Test updates in staging

4. **Monitoring**
   - Track deployment status
   - Monitor Pod health
   - Set up alerts

## Common Commands

```bash
# View deployments
kubectl get deployments

# View deployment details
kubectl describe deployment nginx-deployment

# View rollout status
kubectl rollout status deployment/nginx-deployment

# View rollout history
kubectl rollout history deployment/nginx-deployment

# Pause a rollout
kubectl rollout pause deployment/nginx-deployment

# Resume a rollout
kubectl rollout resume deployment/nginx-deployment
```
