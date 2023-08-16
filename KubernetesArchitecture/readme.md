
# Kubernetes Architecture
> A Basic Kubernetes architecture consists of 2 main parts: 
> 1.	[Master Node] - A control plane (Kubernetes control plane) 
> 2.	[Worker Node] - Cluster nodes (Kubelets, also called minions). 

> Kubernetes Control Plane or [Master Node] consists of following components
> 1.	Kubernetes API server 
> 2.	Kubernetes scheduler
> 3.	Kubernetes controller manager
> 4.	etcd 

> Kubernetes Cluster Nodes or [Worker Nodes] consists of following components
> 1.	Container runtime engine or docker
> 2.	A Kubelet service
> 3.	A Kubernetes proxy service.


# Kubernetes Control Plane [Master Node]  

> - Master Node is also called as Kubernetes Control Plane or Head Node. The control plane is the nerve center that manages the components and controls the cluster. It also maintains a data record of the configuration and state of all the cluster’s Kubernetes objects. Control Plane acts as Master and It’s possible to have a one or more master nodes (for high availability), but by default there is a single master server which acts as a controlling node and point of contact. 
> - The Kubernetes control plane is in constant contact with compute machines to ensure that the cluster runs as configured. Controllers respond to change in cluster and manages object states and constantly checks if current state of system objects is same as the desired state or specification. Worker nodes are where your apps are installed, but they are managed by master nodes
> - Major components comprise the control plane are - the API server, the scheduler, the controller-manager, and etcd. These core Kubernetes components ensure containers are running with the necessary resources in sufficient numbers. These Control Plane can work on one primary Master node, but in-order to achieve fault tolerance, we replicate them across multiple Master nodes to achieve high availability. 
> - Kubernetes works on Declarative model. We give API Server a manifest file that describes the end or desired state and then Kubernetes does all the things which are necessary to reach to the desired state  



