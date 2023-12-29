# Kubernetes notes

## Components

### Master node

* api server (ui, rest, cli)
* controller manager - manging container lifecycles
* scheduler - which worker node the next container should run on
* etcd - kv backing store, stores state of each worker node and container. Backup and restore are made from etcd snapshots


### VPC

* virtual network that provides a unified view of the resources contained in the worker nodes

### worker nodes

* Where the containers run
* kubelet process
* beefy machines typically


### Pod

* Smallest unit in kubernetes
* Provides a abstraction over a container, you don't work with docker directly,
* 1 app per pod
* each pod gets its own IP address
* pods communicate with each other using these ip addresses
* when is recreated, it will have different ip address
* typically you don't work with pods directly, you use Deployments to define your service
* app must be stateless

### Service

* Has a permanent IP
* Runs one or more pods
* Pods can restart within the service, but IP of service will remain unchanged
* Can be external service (can be accessed from outside k8s) or internal 
* it's also a load balancer and will distribute requests across pods

### Ingress

* Sits on top of a service, provides the external access point to a service
* also provides ssl termination


### ConfigMap

* Basically externalised env vars to map things like service names to config vars


### secret

* Just like ConfigMap but secure storage


### Volumes

* Connects physical storage to a pod
* Can be on the host itself, or remote
* Like a external harddrive being plugged into the kubernetes cluster
* Kubernetes doesn't manage data persistence!!


### Deployments

* Defines a set of services and auto scaling paraeters

### StatefulSet

* Service abstraction for stateful apps like databases
* Difficult to work with, databases are typically managed outside of kubernetes



### kubectl

* Commandline interface to the API server that runs on the master node

