# [k8s](https://github.com/kubernetes/kubernetes) on [multipass](https://github.com/canonical/multipass)
easy local kubernetes cluster set-up for certification preparation via multipass, cloud init and kubeadm

## Windows via powershell

1. k8s control plane: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-plane.yaml' | Select-Object -Expand Content | multipass launch -n k8s-control-plane --cpus 2 --mem 2G 18.04 --cloud-init -
```
2. k8s worker node 1: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/worker-node-1.yaml' | Select-Object -Expand Content | multipass launch -n k8s-worker-1 --cpus 2 --mem 4G --disk 10G 18.04 --cloud-init -
```
3. k8s worker node 2: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/worker-node-2.yaml' | Select-Object -Expand Content | multipass launch -n k8s-worker-1 --cpus 2 --mem 4G --disk 10G 18.04 --cloud-init -
```

## Linux/MAC

1. k8s control plane: 
```
curl https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-plane.yaml | multipass launch -n control-plane --cpus 2 --mem 2G 18.04 --cloud-init -
```
2. k8s worker node 1: 
```
curl https://raw.githubusercontent.com/ab2k/k8s-multipass/main/worker-node-1.yaml | multipass launch -n k8s-worker-1 --cpus 2 --mem 4G --disk 10G 18.04 --cloud-init -
```
3. k8s worker node 2: 
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
4. add any desirable CNI, or just use [Project Calico](https://github.com/projectcalico/calico) manifest
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```
5. get join token to use on worker nodes
```
kubeadm token create --print-join-command
```

## Set-up worker nodes with 10.10.10.1 as a control-plane ip 
```
sudo kubeadm join ...
```

## and thats it :) enjoy!
