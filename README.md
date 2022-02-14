# k8s-multipass
k8s multipath cloud init files

## windows via powershell

1. k8s control plane: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-plane.yaml' | Select-Object -Expand Content | multipass launch -n control-plane --cpus 2 --mem 2G 18.04 --cloud-init -
```

## linux/mac

1. k8s control plane: 
```
curl https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-plane.yaml | multipass launch -n control-plane --cpus 2 --mem 2G 18.04 --cloud-init -
```
