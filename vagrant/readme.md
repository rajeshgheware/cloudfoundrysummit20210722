First get two ubuntu machines
vagrant up  


apt-get update && apt-get install -y kubelet=1.20.0-00 kubeadm kubectl

# https://github.com/kubernetes/kubernetes/issues/45487
echo 'User=root' >> /etc/systemd/system/kubelet.service.d/10-kubeadm.conf

systemctl daemon-reload
systemctl enable kubelet && systemctl restart kubelet
systemctl enable docker && systemctl restart docker

sudo kubeadm init --apiserver-advertise-address 192.168.26.10 --pod-network-cidr 10.244.0.0/16

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

kubeadm token create --print-join-command

