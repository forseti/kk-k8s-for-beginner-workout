# `minikube`

`minikube` is a local Kubernetes for learning and developing on Kubernetes.

## Installing `kubectl`
### Download `kubectl`
```shell
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

### Download the `kubectl` checksum file:
```shell
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

### Validate the `kubectl` against the checksum file:
```shell
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

if valid, the output is:
```shell
kubectl: OK
```

Otherwise, a nonzero status will be printed:
```shell
kubectl: FAILED
sha256sum: WARNING: 1 computed checksum did NOT match
```

###  Install `kubectl` on the `/usr/local/bin` directory
```shell
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

If you do not have root access, `~/.local/bin` can be used:
```shell
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
# and then append (or prepend) ~/.local/bin to $PATH
```

###  Test the installation
```shell
kubectl version
```

## Installing `virtualbox`

###  Edit `/etc/apt/sources.list` and add the repo
```shell
deb [arch=amd64 signed-by=/usr/share/keyrings/oracle-virtualbox-2016.gpg] https://download.virtualbox.org/virtualbox/debian <mydist> contrib
```

### Download the public key.
```shell
wget -O- https://www.virtualbox.org/download/oracle_vbox_2016.asc
```

### Verify the public key with GPG
```shell
gpg --show-keys oracle_vbox_2016.asc
```

### Install `virtualbox`
```shell
sudo apt-get update
sudo apt-get install virtualbox
```

## Installing `minikube`
Check if virtualization is enabled:
```shell
grep -E --color 'vmx|svm' /proc/cpuinfo
```

### Download `minikube`
```shell
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

### Install `minikube`
```shell
chmod +x minikube
cp minikube ~/.local/bin
```

### Run `minikube` on `virtualbox`
```shell
minikube start --driver=virtualbox
```

### Check the minikube status
```shell
minikube status
```
Output:
```text
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```

### Check nodes with `kubectl`
```shell
kubectl get nodes
```
Output:
```text
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   11m   v1.28.3
```

### Create deployment
```shell
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
```
Output:
```text
deployment.apps/hello-minikube created
```

### Expose deployment
```shell
kubectl expose deployment hello-minikube --type=NodePort --port=8080
```
Output:
```text
service/hello-minikube exposed
```

### Get the service info with `kubectl`
```shell
kubectl get services hello-minikube
```
Output:
```text
NAME             TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
hello-minikube   NodePort   10.105.191.27   <none>        8080:31213/TCP   17s
```

### Get the URL of the service
```shell
minikube service hello-minikube
```
Output:
```text
|-----------|----------------|-------------|-----------------------------|
| NAMESPACE |      NAME      | TARGET PORT |             URL             |
|-----------|----------------|-------------|-----------------------------|
| default   | hello-minikube |        8080 | http://192.168.59.100:31213 |
|-----------|----------------|-------------|-----------------------------|
```

### Delete the service
```shell
kubectl delete services hello-minikube
```
Output:
```text
service "hello-minikube" deleted
```

### Delete the deployment
```shell
kubectl delete deployment hello-minikube
```
Output:
```text
deployment.apps "hello-minikube" deleted
```