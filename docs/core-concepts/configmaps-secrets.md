# ConfigMaps and Secrets

ConfigMaps and Secrets are Kubernetes objects used to store configuration data and sensitive information separately from application code.

## ConfigMaps

### What are ConfigMaps?
- Store non-confidential data
- Key-value pairs
- Can be mounted as volumes
- Can be used as environment variables

### Creating ConfigMaps

#### 1. From Literal Values
```bash
kubectl create configmap my-config --from-literal=key1=value1 --from-literal=key2=value2
```

#### 2. From File
```bash
kubectl create configmap my-config --from-file=path/to/file
```

#### 3. From Directory
```bash
kubectl create configmap my-config --from-file=path/to/directory
```

### Using ConfigMaps

#### 1. As Environment Variables
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: my-image
    envFrom:
    - configMapRef:
        name: my-config
```

#### 2. As Volume
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: my-image
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: my-config
```

## Secrets

### What are Secrets?
- Store sensitive data
- Base64 encoded
- Encrypted at rest (with proper configuration)
- More secure than ConfigMaps

### Types of Secrets
1. Opaque (generic)
2. docker-registry
3. tls
4. service-account-token

### Creating Secrets

#### 1. From Literal Values
```bash
kubectl create secret generic my-secret --from-literal=username=admin --from-literal=password=secret
```

#### 2. From File
```bash
kubectl create secret generic my-secret --from-file=path/to/file
```

#### 3. TLS Secret
```bash
kubectl create secret tls my-tls --cert=path/to/cert --key=path/to/key
```

### Using Secrets

#### 1. As Environment Variables
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: my-image
    env:
    - name: SECRET_USERNAME
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: username
```

#### 2. As Volume
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: my-image
    volumeMounts:
    - name: secret-volume
      mountPath: /etc/secret
  volumes:
  - name: secret-volume
    secret:
      secretName: my-secret
```

## Best Practices

### 1. ConfigMap Best Practices
- Use descriptive names
- Group related configurations
- Document configuration options
- Version control configuration files

### 2. Secret Best Practices
- Never store in version control
- Use proper encryption
- Rotate secrets regularly
- Limit access to secrets
- Use RBAC for secret access

### 3. Security Considerations
- Use network policies
- Implement proper access control
- Monitor secret access
- Use encryption at rest

## Common Commands

```bash
# List ConfigMaps
kubectl get configmaps

# List Secrets
kubectl get secrets

# Describe ConfigMap
kubectl describe configmap my-config

# Describe Secret
kubectl describe secret my-secret

# Delete ConfigMap
kubectl delete configmap my-config

# Delete Secret
kubectl delete secret my-secret
```

## Next Steps

Learn about [Getting Started](../getting-started/installation.md) with Kubernetes to put these concepts into practice. 