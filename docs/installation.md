# Create an account and Login into GCP:
https://console.cloud.google.com/start

# Create 3 VM'S (1 Master, 2 Worker) in GCP using below settings
Compute Engine -> Create VM's
Master Node configuration (Memory 2 GB - CPU 2)
Worker Nodes configuration (Memory 1 GB - CPU 2)
Boot -> Ubuntu
Access -> Allow full access to all cloud APIS
Firewall -> Allow HTTP/HTTPS Traffic

# Create Firewall rule to open up all ports using below settings (suitable only for local development)
Targets - All instances in the network.
Source IP4 range - 0.0.0.0/0
Protocols and Ports - Allow All

# SSH in to all nodes and execute below commands (Ubuntu)
sudo apt-get update
sudo apt-get install -y apt-transport-https
sudo apt-get install -y ca-certificates
sudo apt-get install -y curl
sudo apt-get install -y software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update ; clear
sudo apt-get install -y docker-ce
sudo vi /etc/docker/daemon.json
{
"exec-opts": ["native.cgroupdriver=systemd"]
}
sudo service docker restart
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-get update ; clear
sudo apt-get install -y kubelet kubeadm kubectl	

# SSH in to Mater Node and execute below commands (Ubuntu)
sudo kubeadm init --ignore-preflight-errors=all
# Copy the kubeadm join command created from above step it has to executed in worker nodes
sudo mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
kubectl get nodes
kubectl get all --all-namespaces

# SSH in to Worker nodes and execute Kubeadm command from step 38
sudo kubeadm join **********************

# Validation in Matser node
kubectl get nodes (You should get below master/worker nodes details)
kubectl get pods -A -o wide
service kubelet status