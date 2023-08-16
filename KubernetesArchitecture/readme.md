
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


## Kubernetes Control Plane  [Kubernetes API Server]
### Process 1 – API Server 
> - The API Server is the frontend and of Kubernetes Control Plane handling internal and external requests.
Its like a cluster gateway which gets request or queries from any client. 
> - The API server acts as a gatekeeper for authentication. When a client makes a request, api server validates and authenticates the request and determines if a request is valid or not. If it is, then only it processes the request. 
> - When we issue commands to the cluster, it is sent to API Server. API Server acts as a central management entity that receives all REST requests for modifications (to pods, services, replication sets/controllers and others). Even Cluster nodes and apps that running on the nodes, if they need to communicate to control plane then they need to talk to API Server
> - API Server can be accessed through REST calls, through the kubectl command-line interface, or through other command-line tools such as kubeadm. 
> - Also, this is the only component that communicates with the etcd cluster, making sure data is stored in etcd and is in agreement with the service details of the deployed pods. Kubectl is a GO language binary. Exposes the API (REST). Consumes JSON/YAML.


## Kubernetes Control Plane  [Kube-Scheduler]
### Process 2 – Kube Scheduler 
> - The Primary responsibilities of Kube Scheduler is to check whether the cluster is healthy. It checks if new containers are needed, If so where will they fit?
> - The scheduler considers the resource needs of a pod, such as CPU or memory, along with the health of the cluster. Then it schedules the pod to an appropriate compute node.
> - It is a service in master responsible for distributing the workload. It is responsible for tracking utilization of working load on cluster nodes and then placing the workload on which resources are available and accept the workload. In other words, this is the mechanism responsible for allocating pods to available nodes.
> - Scheduler is responsible for starting application pods on one of the worker node.
> - It’s a component on the Master that watches newly created pods that have no nodes assigned and selects a node for them to run on. It first checks for the availability of the resources in nodes, and based on the type of request, it assigns one that’s available. The scheduler obtains all this information from etcd, via the api server.
> - Scheduling decisions are based on resource availability and other factors like hardware, software, workload, and policy constraints. All these factors together ensure that a node is suitable for a pod to run. The kube-scheduler is the one responsible for managing the timely service of the whole Kubernetes infrastructure.

## Kubernetes Control Plane  [Kube Controller Manager]
### Process 3 – Kube Controller Manager . 
> - A Kube Controller Manager can be considered as a daemon which runs in nonterminating loop and is responsible for collecting and sending information to API server.
> - It acts as a control loop that regulates the state of the cluster and continuously monitors the cluster for any change and then it sends instructions to make changes to bring the current status of the cluster to the desired state.
> - Whenever the pods die inside a node there must be a way to reschedule those pods. Controller manager detects cluster state changes like crashing of pods and tries to recover the cluster state as soon as possible. And for that it makes request to Scheduler to reschedule those pods
> - Controller Manager consists of 2 main controllers – 
> 1.	Kube Controller manager 
> 2.	Cloud Controller manager 

> Kube Controller manager 
> Components of kube controller manager – 
> 1.	Node controller – monitoring the node
> 2.	Replication controller – maintains correct number of pods 
> 3.	Endpoints controller – maintains all the services and communications
> 4.	Service account controller and token controller – creates default accounts and api access tokens for new namespaces

> - These controllers are responsible for overall health of the cluster
> - Ensures nodes are running all the time and schedules new nodes if it dies.
> - Correct number of pods are running as per spec file
> - Logically each controller is a separate process, they are all compiled into a single binary and run in a single process.

> Cloud Controller manager –
> - Cloud Controller Manager interacts with the cloud-specific APIs. It interacts with the underlying infra of cloud provider. It Manages storage volumes, load balancing and routing.
> - It can be used to add scale a cluster by adding more nodes on cloud VMs, and leverage cloud provider high availability and load balancing capabilities to improve resilience and performance.
> - Additionally, it helps decouple the Kubernetes cluster from components that interact with a cloud platform, so that elements inside the cluster do not need to be aware of the implementation specifics of each cloud provider.
> Components of cloud controller manager 
> 1.	Node controller – checks with cloud provider if node has been deleted after it stops responding.
> 2.	Route controller – for setting up routes in the underlying cloud infra
> 3.	Service controller – for creating updating cloud provider load balancers.
> 4.	Volume manager – for creating attaching and mounting volumes and interacting with the cloud provider to orchestrate volumes.


## Kubernetes Control Plane  [etcd]
### Process 4 – etcd 
> - etcd is an open source, distributed, high availability and fault tolerant key value database(store) of a cluster state. Its like a cluster brain.
> - etcd is the database system that’s used for storing cluster state, cluster configuration, networking information, and other persistent information.
> - It stores the data in key – value pair.
> - When an update is needed, it doesn’t overwrite the pairs; rather, it creates a new entry and appends the end, and marks the previous entry for future removal. Each and every change in cluster like when a new pod is scheduled or when a pod dies all of these gets stored in a key value store ie etcd.
> - Out of all the master components only API server can communicate with the etcd data store. Every update that you make in the database travels through the kube-api server.
> - One interesting thing to note here is that if you have simultaneous requests to update a value in the database, all these requests go to kube-apiserver, which then passes them to the etcd database. The first request would easily be processed, but the second one (with the previous version number) would not be available since the object is rewritten by the first request.


# Kubernetes Cluster Nodes [also called as Node or Minions or Worker Nodes] 

> - When we deploy Kubernetes cluster it has atleast one Master node and multiple Worker nodes. Worker node will have one or more PODs and PODs will have one or more containers. The Master node manages both Worker nodes and PODs
> - Worker Nodes can be any physical or Virtual Machine where you can run containerized workloads or where containers can be deployed. The worker nodes are where the actual application is deployed.
> - Consider there is one node and in it there are 2 application pods running on it. Each Node has multiple pods running on it. There must be 3 processes installed on every node to schedule and manage those pods. Worker Nodes do the actual work.
> - Worker nodes are generally more powerful than master nodes because they have to run hundreds of clusters on them. However, master nodes hold more significance because they manage the distribution of workload and the state of the cluster.


## Kubernetes Cluster Nodes  [Container Runtime (Docker)]
### Process 1 – Container Runtime    
> - Each node contains a container runtime engine, which is responsible for running containers
> - K8s supports various container runtimes like Docker, containerd, Cri-o, Rketlet, Kubernetes CRI (container runtime interface)
> - Interestingly, Kubernetes does not directly support Docker, and in recent versions Kubernetes has deprecated Docker support. The reason is that Docker does not fully support CRI. It is technically possible to run Docker with Kubernetes, but in most cases, Kubernetes runs with other, lightweight container engines that are more suitable for fully-automated operations.


## Kubernetes Cluster Nodes  [Kubelet]
### Process 2 – Kubelet   
> - Kubelet is a process that runs on each node. It can communicate with the Kubernetes control plane[API Server] and executes the actions specified by the control plane ie. API Server.
> - Kubelet interacts with both ie the container and node as well. Kubelet starts the pod with a container inside and then assigning resources from that node to the container like CPU/RAM/Storage etc)
> - It schedules the pods and containers and makes sure containers are running inside the pod. When Kubernetes wants to schedule a pod on a specific node, it sends the pod’s PodSecs to the kubelet. The kubelet reads the details of the containers specified in the PodSpecs, pulls the images from the registry and runs the containers. From that point onwards, the kubelet is responsible for ensuring these containers are healthy and maintaining them according to the declarative configuration.
> - Kubelet does not manage any container that is not created by Kubernetes.



## Kubernetes Cluster Nodes  [Kube Proxy]
### Process 3 – Kube Proxy   
> - Kube proxy is a network agent which runs on each node responsible for maintaining network configuration and rules. Its a proxy service to deal with individual host subnetting and expose services to the external world.
> - It makes sure every pod gets its own unique IP
> - All worker nodes run a daemon called kube-proxy which is a network proxy which watches the api server on the master node for the addition and removal of services and endpoints. Kube Proxy is responsible for forwarding requests from services to pods
> - kube-proxy enables networking on Kubernetes nodes, with network rules that allow communication between pods and entities outside the Kubernetes cluster. kube-proxy either forwards traffic directly or leverages the operating system packet filtering layer.
> - kube-proxy can run in three different modes: iptables, ipvs, and userspace (a deprecated mode that is not recommended for use). iptables, the default mode, is suitable for clusters of moderate size, however it uses sequential network rules which can impact routing performance. ipvs can support a large number of services, as it supports parallel processing of network rules.
> - It helps in forwarding the request to correct containers and is capable of performing primitive load balancing. It makes sure that the networking environment is predictable and accessible and at the same time it is isolated as well. 


### Addons

> Addons use Kubernetes resources (DaemonSet, Deployment, etc) to implement cluster features. Because these are providing cluster-level features, namespaced resources for addons belong within the kube-system namespace. In short, add-ons extend the functionality of Kubernetes. 
> - DNS - Cluster DNS is a DNS server, in addition to the other DNS server(s) in your environment, which serves DNS records for Kubernetes services.
> - While the other addons are not strictly required, all Kubernetes clusters should have cluster DNS, as many examples rely on it. It provides a lightweight mechanism in service discovery. Containers started by Kubernetes automatically include this DNS server in their DNS searches.
> - Web UI (Dashboard) - Dashboard is a general purpose, web-based UI for Kubernetes clusters. It allows users to manage and troubleshoot applications running in the cluster, as well as the cluster itself.
> - Container Resource Monitoring - Container Resource Monitoring records generic time-series metrics about containers in a central database, and provides a UI for browsing that data.
> - Cluster-level Logging - A cluster-level logging mechanism is responsible for saving container logs to a central log store with search/browsing interface


## Other Kubernetes Components

### Ingress 
> The request we make from browser first goes to ingress and ingress then forwards it to Service.
> https://myapp.com    is the ingress and ingress reroutes it to http://124.89.10.12:8080 which is basically a service.

### ConfigMap  
> Its an external configuration of the application.
> It contains configuration data of urls of database or some other services we use.

### Secret 
> Secret is same as configMap but it is used to store secret data like db username and db password or other credentials.
> Data is not stored in plain text format but in base64 encoded

### Volumes 
> It attaches physical storage on harddrive to your pod to the local hardrive or cloud storage or other VM etc
> Kubernetes/k8s cluster is not responsible for managing the data and storing it persistently. We as an administrator are responsible for managing and storing and replicating the data.
> It is similar to a container volume in Docker, but a Kubernetes volume applies to a whole pod and is mounted on all containers in the pod. Kubernetes guarantees data is preserved across container restarts. The volume will be removed only when the pod gets destroyed. Also, a pod can have multiple volumes (possibly of different types) associated.

### Namespace 
> In Kubernetes cluster we can organize resources in namespaces
> Namespace is a virtual cluster (a single physical cluster can run multiple virtual ones) intended for environments with many users spread across multiple teams or projects, for isolation of concerns.
> Resources inside a namespace must be unique and cannot access resources in a different namespace. Also, a namespace can be allocated a resource quota to avoid consuming more than its share of the physical cluster’s overall resources.
> There are 4 namespaces by default
> Namespace helps in – Structuring your components
> Avoid conflicts between teams
> Share services between different environments
> Access and resource limits on namespaces level


### StatefulSet 
> Deployment is only used to create stateless apps where as for statefull thing like databases there is another Kubernetes component which is used to create and manage it which is StatefullSet.
> StatefulSet just like Deployment take care of replicating the PODS and scaling them up or down but making sure that database reads and writes are synchronized so that there are no db inconsistencies left

### Helm
> Package manager for Kubernetes – To package yaml files and distribute them in public and private repositories
> Create your own Helm chart with Helm
> Push it to repository to make it available to others
> Download and use existing helm chart created by others
> Helm can help you define a common Blueprint for all the microservices
> Dynamic values can then be replaces by placeholders in blueprint


### POD
> Pod is the smallest unit of management in a Kubernetes cluster. In VMware world the atomic unit of deployment is the Virtual Machine, In docker world it is container and in Kubernetes world it is POD.
> The unit of scaling in Kubernetes is POD. If we want to scale our app which is in Kubernetes environment, then we do it by adding and removing pods. We never scale the app by adding the more of same containers to an existing pod
> A Kubernetes cluster consists of one or more Master node and multiple worker nodes.
> A pod includes one or more containers, and operators can attach additional resources to a pod, such as storage volumes.
> Pod – generally refers to one or more containers that should be controlled as a single application. Usually, we should run 1 container per pod but we can have multiple containers inside same pod.
> The Kubernetes Scheduler, running on the master node, is responsible for searching for eligible worker nodes for each pod and deploying it on those nodes.
> Kubernetes runs or orchestrates containers, only those containers should always run inside a pod.
> In Kubernetes we do not interact with containers directly or we cannot directly deploy container in Kubernetes without a pod
> A Pod is a functional unit ie. just a thin wrapper around every container.
> A POD can have a single or multiple containers and PODs are housed inside Node. A Node can have single POD or multiple PODs.
> Technically a Pod is a Shared execution Environment. An Execution Environment is a collection of all the necessary things that an app needs to run.
> All the multiple containers running inside a POD share that Execution Environment of that POD.
> Eg- If there are 2 containers running inside a pod then they both will share the same pods IP. Since both containers are sharing the same IP, if we want to connect to either container from the outside then because they are on same IP, you have to map to them to unique ports. Inside the POD if the containers want to communicate with each other then they can use the unique ports over the Pods localhost interface
> Pods can be connected to persistent storage to run stateful applications.
> A pod is shown up and running only once all the containers inside that pod are up and running.
> Pods are Mortal and stateless by design, meaning they are dispensable and replaced by an identical unit if one fails. Each time when POD crashes or dies, the deployment controller spins up new pod identical to the one that just died and IP address for that POD changes on its recreation. Its not the dead pod is repaired and brought up live again.
> Kubernetes offers its own virtual network. Each POD gets its own IP address, not the container. Each POD can communicate with each other with that IP address(internal IP address and not a public one)
> Service Mesh – An additional container is injected into every pod we deploy to a cluster. The job of service mesh container is to sit in between the app container and entrance of pod ie the network, so that it can encrypt and decrypt the traffic coming and leaving the pod and other telemetry stuff.
> Kubernetes gives PODS their own IP addresses and a single DNS name for a set of PODs, and can load balance across them. With this system, Kubernetes has complete control over network and communication between pods and can load balance across them.


### Nodes
> Node is a Server. Either physical server or a virtual server.
> There can be multiple nodes in a Kubernetes cluster and they can spread across different data centers
> Inside node there is pod When a pod dies a new pod arrives with new IP. Also when we scale up the PODs, all the newly added pods are also having new and different Ips. When we scale down then we may shut the pods which clients might be using. So depending on PODs IP is very unreliable and risky. To solve this problem we have service object which sits in front of the pods and provides a stable IP and DNS name 



### Service   
> A Kubernetes service is a set of pods that work together. PODs that have same set of functions are abstracted into sets called services.
> A same single service can be run via multiple pods.
> When a pod dies a new pod arrives with new IP. Also when we scale up the PODs, all the newly added pods are also having new and different Ips. When we scale down then we may shut the pods which clients might be using. So depending on PODs IP is very unreliable and risky. To solve this problem we have service object which sits in front of the pods and provides a stable IP and DNS name
> Service also acts does light weight load balancing. The single IP and DNS name of service object load balances the requests it receives to the pods sitting behind it
> The stable DNS name and IP address is never changed and its permanent. Service’s IP address and DNS name is different from POD. PODs have their own IP address and pod can die, if new pod replaces old one then it will have its own new IP address
> Services send traffic to only healthy pods. They can send traffic to endpoints outside the cluster
> PODs communicate with each other with help of service
> Service – pods are volatile, that is Kubernetes does not guarantee a given physical pod will be kept alive (for instance, the replication controller might kill and start a new set of pods). Instead, a service represents a logical set of pods and acts as a gateway, allowing (client) pods to send requests to the service without
needing to keep track of which physical pods actually make up the service.
> Each POD has its own Service. Lifecycles of POD and services are not connected, so even if pod dies the service and its IP address will stay.
> External service – is a service which we create inorder to open services to external sources(open application in browser)
> Internal Service is service which we create inorder to communicate internally within a node


### Labels and Selectors
> Every POD can have labels added on it and similarly the Service will have selectors added on it.
> If the labels added on pods matches with selectors added on service, then the service will divert the traffic to those pods. If we manually add our own extra pod with same label as selector then service will load balance traffic to that pod as well.
  
> How labels and selectors help us - Lets say we have a new version of our app and we want to push it to production – Our current environment is running on version say 1.3 and we want to update it to 1.4. The way we can do this is – we include new pods with new version along with older pods with old versions
  
> The selector is having 2 labels which matches the new versions as well as old versions of pod. So the new connection requests will hit to old pods as well as new pods.
> Now instead of deleting the old pods we can simply add and additional selector on service for new version so that service will load balance traffic only on new pods ie new version of app while the old version pods are still running and they wont get any traffic
> This way if we wish to roll back any changes we can do that by just changing the label on service and its done.


### Deployment
> Blueprint of our pod is known as Deployments.
> Since pod is a layer of abstraction on top of containers, here deployment is another layer of abstraction on top of pods
> In practice we don’t create pods, we create deployments in which we describe the desired state of a pod or a replica set, in a yaml file. The deployment controller then gradually updates the environment (for example, creating or deleting replicas) until the current state matches the desired state specified in the deployment file.
> For example, if the yaml file defines 2 replicas for a pod but only one is currently running, an extra one will get created. Note that replicas managed via a deployment should not be manipulated directly, only via new deployments.
> The yaml file is read by apiserver and then, the apiserver then transfers this info to deployment controller and the DC quickly provisions the components we had asked for.
> If a pod dies or crashes abruptly then the desired state and current state are in mismatch. The responsibility of maintaining exact number of pods is with replicaset controller which manages the replicas of pod.   

------------------------
In the most basic cluster there can be 2 master nodes and 3 worker nodes. As the demand increase we can add more nodes in our cluster. The way we add new master node is like we should get a new bare server, then install all the master processes on it and add it to the Kubernetes cluster. And if we want to add new worker nodes then similar process like master one just install worker processes instead of master processes and add it to the cluster

> MiniKube – Minikube is a 1 node cluster where the master processes and the worker processes both run on one node.
It creates virtual box on your laptop and node runs in that virtual box. It’s a one node K8S cluster and it can be used for testing purpose.
> Kubectl – Cmd line tool for Kubernetes cluster    


### Kubernetes deployment Strategies
> Ramped - Kubernetes’s default rollout method is a ramped or rolling deployment. This deployment slowly replaces pods one at a time to avoid downtime. Old pods are scaled down only after new pods are ready. If your deployment encounters problems, you can pause or cancel the Kubernetes deployment without taking the entire cluster offline.
> Blue/green - In a blue/green deployment, you release a new version (blue) of your application or workflow while your current version (green) is still running. This allows you to test the blue version in production while only exposing users to the green, stable version. Once tested, the blue version gradually replaces the green version.
> Canary - Allow your customers to test your Kubernetes deployment by releasing the new version to a small group of them. You’ll run one ReplicaSet of the new version along with the current version and then, after a specified period of time without errors, scale up the new version as you remove the old version.
> A/B testing - Much like the canary Kubernetes deployment strategy, an A/B testing strategy targets a specific group of customers. However, an A/B testing deployment seeks to establish more than the stability of a version—it’s used to test how effective the version is at achieving business goals. The new version is distributed to users based on factors like cookies, geolocation, operating system, and device type, and it’s frequently run alongside the current version—scaling up as the new version proves its worth.



> Process of deploying an APP to Kubernetes
> - You start with App code
> - Build it into a container image
> - Store that in a repo
> - Define it in a Kubernetes manifest
> - And then post that to API server















> Kubernetes Nodes vs Pods
> A Kubernetes node is a single machine in a cluster that serves as an abstraction. Instead of managing specific physical or virtual machines, you can treat each node as pooled CPU and RAM resources on which you can run containerized workloads. When an application is deployed to the cluster, Kubernetes distributes the work across the nodes. Workloads can be moved seamlessly between nodes in the cluster.
