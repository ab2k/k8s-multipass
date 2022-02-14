# k8s-multipass
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
