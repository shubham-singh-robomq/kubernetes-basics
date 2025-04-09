# Basic Commands

This guide covers essential Kubernetes commands for managing your cluster and applications.

## Cluster Information

### 1. Cluster Status
```bash
# Check cluster status
kubectl cluster-info

# Get cluster nodes
kubectl get nodes

# Get detailed node information
kubectl describe nodes
```

### 2. Version Information
```bash
# Client and server version
kubectl version

# Server version only
kubectl version --short
```

## Working with Pods

### 1. Pod Management
```bash
# List all pods
kubectl get pods

# List pods with more details
kubectl get pods -o wide

# List pods in all namespaces
kubectl get pods --all-namespaces

# Get pod details
kubectl describe pod <pod-name>

# Delete a pod
kubectl delete pod <pod-name>
```

### 2. Pod Logs
```bash
# View pod logs
kubectl logs <pod-name>

# Follow logs
kubectl logs -f <pod-name>

# View logs of a specific container
kubectl logs <pod-name> -c <container-name>
```

### 3. Pod Interaction
```bash
# Execute command in pod
kubectl exec <pod-name> -- <command>

# Get interactive shell
kubectl exec -it <pod-name> -- /bin/bash

# Copy files to/from pod
kubectl cp <pod-name>:<path> <local-path>
kubectl cp <local-path> <pod-name>:<path>
```

## Working with Deployments

### 1. Deployment Management
```bash
# List deployments
kubectl get deployments

# Create deployment
kubectl create deployment <name> --image=<image>

# Update deployment
kubectl set image deployment/<name> <container>=<image>

# Scale deployment
kubectl scale deployment <name> --replicas=<number>

# Delete deployment
kubectl delete deployment <name>
```

### 2. Deployment Updates
```bash
# View rollout status
kubectl rollout status deployment/<name>

# View rollout history
kubectl rollout history deployment/<name>

# Rollback to previous version
kubectl rollout undo deployment/<name>

# Rollback to specific revision
kubectl rollout undo deployment/<name> --to-revision=<number>
```

## Working with Services

### 1. Service Management
```bash
# List services
kubectl get services

# Create service
kubectl expose deployment <name> --port=<port> --target-port=<target-port>

# Get service details
kubectl describe service <name>

# Delete service
kubectl delete service <name>
```

### 2. Port Forwarding
```bash
# Forward local port to pod
kubectl port-forward <pod-name> <local-port>:<pod-port>

# Forward local port to service
kubectl port-forward service/<service-name> <local-port>:<service-port>
```

## Working with ConfigMaps and Secrets

### 1. ConfigMap Management
```bash
# Create from literal
kubectl create configmap <name> --from-literal=<key>=<value>

# Create from file
kubectl create configmap <name> --from-file=<path>

# List configmaps
kubectl get configmaps

# Get configmap details
kubectl describe configmap <name>
```

### 2. Secret Management
```bash
# Create from literal
kubectl create secret generic <name> --from-literal=<key>=<value>

# Create from file
kubectl create secret generic <name> --from-file=<path>

# List secrets
kubectl get secrets

# Get secret details
kubectl describe secret <name>
```

## Namespace Management

```bash
# List namespaces
kubectl get namespaces

# Create namespace
kubectl create namespace <name>

# Switch namespace
kubectl config set-context --current --namespace=<name>

# Delete namespace
kubectl delete namespace <name>
```

## Resource Management

### 1. Resource Quotas
```bash
# List resource quotas
kubectl get resourcequotas

# Get quota details
kubectl describe resourcequota <name>
```

### 2. Resource Usage
```bash
# Get resource usage
kubectl top nodes
kubectl top pods
```

## Troubleshooting

### 1. Common Issues
```bash
# Get events
kubectl get events

# Get component status
kubectl get componentstatuses

# Check API resources
kubectl api-resources
```

### 2. Debugging
```bash
# Get detailed object information
kubectl get <resource> <name> -o yaml

# Get logs from all containers
kubectl logs <pod-name> --all-containers

# Check pod events
kubectl describe pod <pod-name>
```

## Best Practices

1. **Command Organization**
   - Use consistent naming
   - Document complex commands
   - Use aliases for common commands

2. **Resource Management**
   - Clean up unused resources
   - Monitor resource usage
   - Use namespaces effectively

3. **Security**
   - Use RBAC
   - Limit access to secrets
   - Follow least privilege principle

4. **Monitoring**
   - Set up logging
   - Configure alerts
   - Track resource usage
