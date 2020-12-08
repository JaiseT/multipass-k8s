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
ssh -i ~/.ssh/multipass ubuntu@172.17.123.253
