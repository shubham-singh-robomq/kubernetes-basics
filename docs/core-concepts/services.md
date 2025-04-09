# Services

Services in Kubernetes provide a stable IP address and DNS name for a set of Pods, enabling network access to your applications.

## What is a Service?

A Service:
- Provides stable networking for Pods
- Enables load balancing
- Supports service discovery
- Handles Pod failures gracefully

## Service Types

### 1. ClusterIP (Default)
- Internal IP address
- Accessible only within cluster
- Basic service type

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```

### 2. NodePort
- Exposes service on each Node's IP
- Accessible from outside cluster
- Static port on each Node

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: MyApp
  ports:
    - port: 80
      targetPort: 9376
      nodePort: 30007
```

### 3. LoadBalancer
- Cloud provider's load balancer
- External IP address
- Automatic load balancing

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: LoadBalancer
  selector:
    app: MyApp
  ports:
    - port: 80
      targetPort: 9376
```

### 4. ExternalName
- Maps service to external DNS name
- No selectors
- No proxying

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: ExternalName
  externalName: my.database.example.com
```

## Service Features

### 1. Load Balancing
- Round-robin by default
- Session affinity support
- Custom load balancing policies

### 2. Service Discovery
- DNS-based discovery
- Environment variables
- Cluster-wide accessibility

### 3. Health Checking
- Endpoint health monitoring
- Automatic endpoint updates
- Failure handling

## Service Management

### 1. Creating Services
```bash
kubectl create -f service.yaml
kubectl expose deployment my-deployment --port=80 --target-port=9376
```

### 2. Viewing Services
```bash
kubectl get services
kubectl describe service my-service
```

### 3. Deleting Services
```bash
kubectl delete service my-service
```

## Advanced Configurations

### 1. Session Affinity
```yaml
spec:
  sessionAffinity: ClientIP
  sessionAffinityConfig:
    clientIP:
      timeoutSeconds: 10800
```

### 2. Multiple Ports
```yaml
spec:
  ports:
  - name: http
    port: 80
    targetPort: 9376
  - name: https
    port: 443
    targetPort: 9377
```

### 3. External IPs
```yaml
spec:
  externalIPs:
  - 80.11.12.10
```

## Best Practices

1. **Service Naming**
   - Use descriptive names
   - Follow naming conventions
   - Include environment if needed

2. **Port Management**
   - Use named ports
   - Document port usage
   - Avoid port conflicts

3. **Security**
   - Use Network Policies
   - Implement proper access control
   - Monitor service access

4. **Monitoring**
   - Track service health
   - Monitor endpoint status
   - Set up alerts

## Common Commands

```bash
# List all services
kubectl get svc

# Get service details
kubectl describe svc my-service

# Create service from deployment
kubectl expose deployment my-deployment --port=80

# Delete service
kubectl delete svc my-service
```
