# Execute the following in all nodes
sudo -i
git clone https://github.com/bolecodex/100-Awesome-Kubernetes-Introduction-Experiments.git
cd 100-Awesome-Kubernetes-Introduction-Experiments/setup-kubernetes-cluster
chmod +x setup-container.sh
chmod +x setup-kubetools-ubuntu.sh
./setup-container.sh
./setup-kubetools-ubuntu.sh

# Execute the following in control node
kubeadm init

# Copy te output and execute the "kubeadm join ..." command in work nodes

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
kubectl get pods --all-namespaces

kubectl cluster-info
kubectl get nodes
