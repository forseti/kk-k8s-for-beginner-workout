# Basic Terminology 
## Worker node
A node is a worker machine, physical or virtual, where containers will be launched by Kubernetes. It is responsible for running the containers and executing the workloads. It is also known as a minion.

## Master Node
A master node is a node that controls/manages a set of worker nodes in a cluster.

## Components
Kubernetes consists of the following components:
* API server (`kube-apiserver`) 
* `etcd`
* Scheduler 
* Controller
* Container runtime
* `kubelet`

#### API Server (`kube-apiserver`)
Users, management devices, and CLIs talk to API server to interact with the Kubernetes cluster.
#### `etcd`
The distributed reliable key-value store used by Kubernetes to store all data used to manage the cluster. etcd is responsible for implementing locks within the cluster to ensure that there are no conflicts between the masters.
#### Scheduler
The scheduler is responsible for distributing work or containers across multiple nodes. It looks for newly create containers and assign them to nodes.
#### Controller
The brain behind orchestrations. They are responsible for noticing and responding when nodes, containers, and endpoints go down. It makes decisions to bring up new containers in such cases.
#### Container runtime
The underlying software that is used to run the containers. In most cases, it's docker. There are other options as well. 
#### `kubelet`
The agent that runs on each node. It is responsible for making sure that the container are running on the nodes as expected.

## Master vs Worker nodes
The differences between a master node and a worker node.
* A master node has the `kube-apiserver`, `etcd`, controller, and scheduler.
* A worker node has the `kubelet` agent and is responsible to communicate with the master node.
  * Providing health info of the worker node.
  * Carrying out actions requested by the master node.

## `kubectl` Utility
This is a command line utility
* Deploy and manage applications on a Kubernetes cluster.
* Retrieve cluster information.
* Retrieve status of other nodes in the cluster.
* And manage other things.

For example:
* `kubectl cluster-info` is for viewing cluster information.
* `kubectl get nodes` is for listing all nodes in the cluster.
* `kubectl run <application>` is used to deploy an application on the cluster.

## Container Runtime Interface (CRI)
Kubernetes' CRI allows any vendor to work as a container runtime for Kubernetes as long as they adhere to Open Container Initiative (OCI) standards. It consists:
* `imagespec`. The specification on how an image should be built.
* `runtimespec`. The specification on how a container runtime should be developed.

`crictl` is a CLI for debugging CRI compatible container runtimes.