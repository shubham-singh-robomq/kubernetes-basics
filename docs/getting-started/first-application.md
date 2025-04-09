# First Application

This guide walks you through deploying your first application on Kubernetes. We'll create a simple web application and expose it to the world.

## Prerequisites

- A working Kubernetes cluster
- kubectl configured to communicate with your cluster
- Basic understanding of Kubernetes concepts

## Step 1: Create a Deployment

Let's create a deployment for a simple web application.

```yaml
# nginx-deployment.yaml
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

Apply the deployment:
```bash
kubectl apply -f nginx-deployment.yaml
```

## Step 2: Verify the Deployment

Check the status of your deployment:
```bash
kubectl get deployments
kubectl get pods
```

## Step 3: Create a Service

Now, let's create a service to expose the deployment:

```yaml
# nginx-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

Apply the service:
```bash
kubectl apply -f nginx-service.yaml
```

## Step 4: Access the Application

### For Cloud Providers
```bash
kubectl get service nginx-service
```
Wait for the external IP to be assigned, then access it in your browser.

### For Minikube
```bash
minikube service nginx-service
```

### For Kind
```bash
kubectl port-forward service/nginx-service 8080:80
```
Then access http://localhost:8080

## Step 5: Scale the Application

Scale the deployment to 5 replicas:
```bash
kubectl scale deployment nginx-deployment --replicas=5
```

## Step 6: Update the Application

Update the nginx image to a newer version:
```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.16.1
```

## Step 7: Monitor the Update

Watch the rollout status:
```bash
kubectl rollout status deployment/nginx-deployment
```

## Step 8: Rollback if Needed

If something goes wrong, rollback to the previous version:
```bash
kubectl rollout undo deployment/nginx-deployment
```

## Step 9: Clean Up

When you're done, clean up the resources:
```bash
kubectl delete deployment nginx-deployment
kubectl delete service nginx-service
```

## Best Practices

1. **Resource Management**
   - Set resource limits and requests
   - Monitor resource usage
   - Implement proper scaling

2. **Health Checks**
   - Add liveness and readiness probes
   - Configure proper timeouts
   - Monitor application health

3. **Security**
   - Use security contexts
   - Implement network policies
   - Follow least privilege principle

4. **Monitoring**
   - Set up logging
   - Configure metrics collection
   - Implement alerts

## Common Issues and Solutions

### 1. Pods Not Starting
- Check resource constraints
- Verify image availability
- Examine pod events

### 2. Service Not Accessible
- Verify service type
- Check network policies
- Ensure proper port mapping

### 3. Update Failures
- Check image availability
- Verify resource constraints
- Monitor rollout status

## Next Steps

Learn about [Basic Commands](basic-commands.md) to manage your Kubernetes applications effectively. 