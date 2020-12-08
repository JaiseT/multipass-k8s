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
