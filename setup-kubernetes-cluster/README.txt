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
# if the command is lost, you can create a new one with "kubeadm token create --print-join-command"

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/master/manifests/calico.yaml
kubectl get pods --all-namespaces

kubectl cluster-info
kubectl get nodes
