# k8s-multipass
k8s multipath cloud init files

## windows (powershell)

1. control-node: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-plane.yaml' | Select-Object -Expand Content | multipass launch -n control-plane -m 2048M 18.04 --cloud-init -
```

## linux/mac

1. control-node: 
```
curl https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-plane.yaml | multipass launch -n control-plane -m 2048M 18.04 --cloud-init -
```
