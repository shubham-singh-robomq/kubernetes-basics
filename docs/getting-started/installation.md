# Installation

This guide covers various methods to install Kubernetes, from local development environments to production clusters.

## Prerequisites

Before installing Kubernetes, ensure you have:
- A supported operating system (Linux, macOS, Windows)
- Minimum 2GB RAM per machine
- 2 CPU cores per machine
- Network connectivity between machines
- Swap disabled (recommended)
- Container runtime installed

## Local Development Options

### 1. Minikube
Minikube is perfect for local Kubernetes development.

#### Installation
```bash
# macOS
brew install minikube

# Linux
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Windows (PowerShell)
choco install minikube
```

#### Starting Minikube
```bash
minikube start
```

### 2. Docker Desktop
Docker Desktop includes a single-node Kubernetes cluster.

#### Installation
1. Download Docker Desktop
2. Enable Kubernetes in settings
3. Start Docker Desktop

### 3. Kind (Kubernetes in Docker)
Kind is a tool for running local Kubernetes clusters using Docker containers.

#### Installation
```bash
# macOS
brew install kind

# Linux
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

#### Creating a Cluster
```bash
kind create cluster
```

## Post-Installation Steps

### 1. Verify Installation
```bash
kubectl version
kubectl get nodes
```

### 2. Install Network Plugin
```bash
# For Calico
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

# For Flannel
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

### 3. Test Cluster
```bash
kubectl run nginx --image=nginx
kubectl get pods
```

## Common Issues and Solutions

### 1. Port Conflicts
- Check for existing services using required ports
- Use different ports or stop conflicting services

### 2. Network Issues
- Verify network connectivity
- Check firewall settings
- Ensure proper network plugin installation

### 3. Resource Constraints
- Increase system resources
- Adjust Kubernetes resource limits
- Optimize container configurations

## Next Steps

After installation, proceed to [First Application](first-application.md) to deploy your first Kubernetes application. 