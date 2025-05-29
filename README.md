Here's your entire setup script properly formatted using triple backticks (` ```bash `) for shell commands and code blocks, with consistent formatting and corrections applied:

```bash
# Update package list and install prerequisites
sudo apt-get update
sudo apt-get install -y ca-certificates curl

# Create directory for Docker's GPG key
sudo install -m 0755 -d /etc/apt/keyrings

# Download Docker’s official GPG key
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add Docker repository to APT sources
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo \"${UBUNTU_CODENAME:-$VERSION_CODENAME}\") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update package index again with Docker repo
sudo apt-get update

# Install Docker Engine and components
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```bash
# Install kubectl
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

# Verify checksum
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

# Install kubectl to /usr/local/bin
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

```bash
# (Optional) Install kubectl without root access
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl

# Add to PATH (append to your shell profile)
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

```bash
# Install Minikube
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
rm minikube-linux-amd64
```

```bash
# Start Minikube cluster
minikube start --force
```

```bash
# Check Minikube and cluster status
minikube status
kubectl get nodes
```


