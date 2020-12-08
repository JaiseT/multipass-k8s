# multipass-k8s

#Create kubernates master
multipass launch bionic \
  --name k8s-controller \
  --cpus 2 \
  --mem 1024M \
  --disk 10G \
  --cloud-init ./cloud-init-k8s.yaml
  
#Create kubernates node1  
multipass launch bionic \
  --name k8s-node1 \
  --cpus 2 \
  --mem 1024M \
  --disk 10G \
  --cloud-init ./cloud-init-k8s.yaml

#Create kubernates node2

multipass launch bionic \
  --name k8s-node2 \
  --cpus 2 \
  --mem 1024M \
  --disk 10G \
  --cloud-init ./cloud-init-k8s.yaml
  
#View VM Instances  
$ multipass list
Name                    State             IPv4             Image
k8s-controller          Running           172.17.123.244   Ubuntu 18.04 LTS
k8s-node1               Running           172.17.123.253   Ubuntu 18.04 LTS
k8s-node2               Running           172.17.123.242   Ubuntu 18.04 LTS  

#Login to controller
ssh -i ~/.ssh/multipass ubuntu@172.17.123.244

#Initialize k8s
sudo kubeadm init --pod-network-cidr=172.17.123.244/16

#Start Cluster
To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  
#Join nodes to cluster 
kubeadm join 172.17.123.244:6443 --token 5z8rqp.je20yaowfuqvq07f \
    --discovery-token-ca-cert-hash sha256:f683ebf1c642eb1374d2ede658c0b529f69581d16d9ffecf0391aa0e7f88c6ee
