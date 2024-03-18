# Basic `kubectl` commands

#### Get the number of nodes
```shell
kubectl get nodes --no-headers | wc -l
```

#### Get the Kubernetes version
```shell
kubectl version | grep -i 'server version'
```

#### Get OS distro/version of the Kubernetes nodes
```shell
kubectl get nodes --no-headers  | awk '{print $1}' | xargs -I {} bash -lc "echo {} - \$(kubectl describe nodes {} | grep -i 'os image')"
```

