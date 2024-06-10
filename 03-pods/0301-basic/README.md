# Pods
* Kubernetes does not deploy containers directly on the worker nodes. 
* The containers are encapsulated into a kubernetes object known as pod.
* A pod is a single instance of an application.
* A pod is the smallest object that you can create in Kubernetes
* Scaling
  * To scale up an application, we can create a new pod 
  with a new instance of the same application.
  * To scale down, we simply delete the new node.
  * The pod will be created in a new node, if the existing node 
  does not have sufficient capacity.
* The pod usually has 1-to-1 relationship with the container that 
is running the application.
* A pod can also have multiple containers but they are usually 
not multiple containers of the same kind.
* A good example of a multi-container pod is when a pod 
have a main container that interact with user requests 
and a helper container that processes data or files uploaded by users.

### Run `nginx` container in a pod
```shell
kubectl run nginx -- image nginx
```
Output:
```text
pod/nginx created
```


### Get available pods
```shell
kubectl get pods
```
Output:
```text
NAME    READY   STATUS              RESTARTS   AGE
nginx   0/1     ContainerCreating   0          3s
```

### Use `-o wide` flag for more additional info, such as IP address
```shell
nginx   1/1     Running   0          4m29s
kubectl get pods -o wide
```
Output:
```text
NAME    READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
nginx   1/1     Running   0          4m34s   10.244.0.4   minikube   <none>           <none>
```

### Get the `pod` description of `nginx`
```shell
kubectl describe pod nginx
```
Output:
```text
Name:             nginx
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.59.100
Start Time:       Mon, 08 Apr 2024 15:30:33 +0800
Labels:           run=nginx
Annotations:      <none>
Status:           Running
IP:               10.244.0.4
...
```