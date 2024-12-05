# kind-setup
# Install Docker
# First, update your package list and download the Docker installation script.
# Visit the official Docker installation page: https://get.docker.com/

# Update package list
```
apt update
```

# Download the Docker installation script
```
curl -fsSL https://get.docker.com -o install-docker.sh
```

# Run the script to install Docker
```
sudo sh install-docker.sh
```


# Install Kind (Kubernetes in Docker)
# Kind is a tool for running local Kubernetes clusters using Docker containers.
# For more info, visit: https://kind.sigs.k8s.io/docs/user/quick-start/

# Download Kind for AMD64 (x86_64 architecture)

```
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.25.0/kind-linux-amd64
```

# Download Kind for ARM64 architecture (optional, if you are using ARM-based systems)

```
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.25.0/kind-linux-arm64
```

# Make the downloaded kind binary executable
```
chmod +x ./kind
```

# Move the Kind binary to /usr/local/bin so it can be accessed globally
```
sudo mv ./kind /usr/local/bin/kind
```

# Create a Kubernetes Cluster with Kind
# Now we will create a custom Kubernetes cluster configuration using a YAML file (k8s.yml).

# Open or create the k8s.yml file using a text editor (e.g., vim).
```
vim k8s.yml
```

# Example k8s.yml content:
# This file defines a Kubernetes cluster with 1 control-plane node and 3 worker nodes.
```
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane   # Control plane node
  - role: worker          # Worker node 1
  - role: worker          # Worker node 2
  - role: worker          # Worker node 3
```


# Create a new Kubernetes cluster using the configuration defined in k8s.yml.
```
kind create cluster --name newcluster --config=k8s.yml
```

# Check that the cluster is created successfully and nodes are ready:
```
docker exec -it newcluster-control-plane /bin/bash
kubectl get nodes
```

# Delete the Cluster
# If you want to delete the created cluster, run the following command:
```
kind delete cluster --name newcluster
```

# Access the Cluster's Control Plane Node
# To access the control plane node of your Kubernetes cluster, use the following command:
```
docker exec -it newcluster-control-plane /bin/bash

```
# Once inside the container, you can update the system and install additional packages like vim.
```
apt update
apt install vim -y   
```
