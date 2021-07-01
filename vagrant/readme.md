# Kubernetes Cluster setup using vagrant

Please review Vagrantfile and run below

`vagrant up`

`sudo kubeadm init --apiserver-advertise-address 192.168.26.10 --pod-network-cidr 10.244.0.0/16`

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

kubeadm token create --print-join-command

