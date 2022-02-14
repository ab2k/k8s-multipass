# k8s-multipass
k8s multipath cloud init files

## windows (powershell)

1. control-node: 
```
Invoke-WebRequest -UseBasicParsing 'https://raw.githubusercontent.com/ab2k/k8s-multipass/main/control-node.yaml' | Select-Object -Expand Content | multipass launch -n k8s-control -m 2048M 18.04 --cloud-init -
```

2. worker-node-1:

3. worker-node-2:

