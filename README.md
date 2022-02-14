# [k8s](https://github.com/kubernetes/kubernetes) via [multipass](https://github.com/canonical/multipass)
k8s multipath cloud init files

## windows via powershell

1. k8s control plane: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-plane.yaml' | Select-Object -Expand Content | multipass launch -n k8s-control-plane --cpus 2 --mem 2G 18.04 --cloud-init -
```
2. k8s worker node 1: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/worker-node-1.yaml' | Select-Object -Expand Content | multipass launch -n k8s-worker-1 --cpus 2 --mem 4G --disk 10G 18.04 --cloud-init -
```
3. k8s worker node 1: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/worker-node-2.yaml' | Select-Object -Expand Content | multipass launch -n k8s-worker-1 --cpus 2 --mem 4G --disk 10G 18.04 --cloud-init -
```

## linux/mac

1. k8s control plane: 
```
curl https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-plane.yaml | multipass launch -n control-plane --cpus 2 --mem 2G 18.04 --cloud-init -
```
2. k8s worker node 1: 
```
curl https://raw.githubusercontent.com/ab2k/k8s-multipass/main/worker-node-1.yaml | multipass launch -n k8s-worker-1 --cpus 2 --mem 4G --disk 10G 18.04 --cloud-init -
```
3. k8s worker node 1: 
```
curl https://raw.githubusercontent.com/ab2k/k8s-multipass/main/worker-node-2.yaml | multipass launch -n k8s-worker-1 --cpus 2 --mem 4G --disk 10G 18.04 --cloud-init -
```

## Set-up control-plane

1. create a cluster
```
sudo kubeadm init --pod-network-cidr 192.168.0.0/16 --kubernetes-version 1.21.0
```
2. copy config to user home directory to utilize kubectl
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
3. add kubectl bash completion
```
echo 'source <(kubectl completion bash)' >>~/.bashrc
```
4. add a CNI to cluster, I will use [Calico Project](https://github.com/projectcalico/calico)
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```
5. get join token
```
kubeadm token create --print-join-command
```

## Set-up worker nodes
```
sudo kubeadm join ...
```

## and thats it :) enjoy!
