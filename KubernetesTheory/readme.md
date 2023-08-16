


# What is Kubernetes

> Kubernetes is an open-source Container orchestration framework/tool or engine that automates deploying, scaling, scheduling, load balancing and  managing containerized application on a group of servers.
>
> Kubernetes orchestrates clusters of virtual machines and schedules containers to run on those virtual machines based on their available compute resources and the resource requirements of each container. Containers are grouped into pods, the basic operational unit for Kubernetes and those pods scale to your desired state.
>
> As applications grow to span multiple containers deployed across multiple servers, operating them becomes more complex. To manage this complexity, Kubernetes provides an open source API that controls how and where those containers will run
>
> Kubernetes also automatically manages service discovery, incorporates load balancing, tracks resource allocation and scales based on compute utilisation. And, it checks the health of individual resources and enables apps to self-heal by automatically restarting or replicating containers
>
> Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services. Its a Container management / Orchestration tool. A container management tool manages containerized applications that facilitates both declarative configuration and automation.
>
> It distributes application workloads across a Kubernetes cluster and automates dynamic container networking needs.
>
> - Kubernetes is a Greek word for Helmsman or captain of a ship
> - Kubernetes was originally developed by Google and later donated to CNCF(Cloud Native Computing Foundation).
> - It is written in Go programming language.
> - Github repo – github.com/kubernetes/kubernetes
> - Like Kubernetes some other container orchestration platforms are Docker Swarm and Apache Mesos Marathon.It manages applications on a platform like Docker



# Why you need Kubernetes and what it can do
> Containers are a good way to bundle and run your applications. In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime. For example, if a container goes down, another container needs to start. Wouldn't it be easier if this behavior was handled by a system?
>
> Keeping containerised apps up and running can be complex because they often involve many containers deployed across different machines. Kubernetes provides a way to schedule and deploy those containers—plus scale them to your desired state and manage their lifecycles. Use Kubernetes to implement your container-based applications in a portable, scalable and extensible way.
>
> That's how Kubernetes comes to the rescue! Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. For example, Kubernetes can easily manage a canary deployment for your system.

> The need for container orchestration tool – 
> -	Trend from monolithic to microservices
> -	Increased usage of containers
> -	Demand for a proper way of managing those hundreds of containers
> Features of container orchestration tool (Kunbernetes)–
> -	High Availability or no downtime 
> -	Scalability or high performance
> -	Disaster Recovery – backup and restore 
> -	Automatic bin packaging
> -	Service discovery and load balancing
> -	Storage orchestration and self healing



# Traditional vs Virtualized vs Containerized Deployments 

  
### Traditional deployment era: 
> Early on, organizations ran applications on physical servers. There was no way to define resource boundaries for applications in a physical server, and this caused resource allocation issues. For example, if multiple applications run on a physical server, there can be instances where one application would take up most of the resources, and as a result, the other applications would underperform. A solution for this would be to run each application on a different physical server. But this did not scale as resources were underutilized, and it was expensive for organizations to maintain many physical servers.
### Virtualized deployment era: 
> As a solution, virtualization was introduced. It allows you to run multiple Virtual Machines (VMs) on a single physical server's CPU. Virtualization allows applications to be isolated between VMs and provides a level of security as the information of one application cannot be freely accessed by another application.Virtualization allows better utilization of resources in a physical server and allows better scalability because an application can be added or updated easily, reduces hardware costs, and much more. With virtualization you can present a set of physical resources as a cluster of disposable virtual machines.Each VM is a full machine running all the components, including its own operating system, on top of the virtualized hardware.
### Container deployment era:
> Containers are similar to VMs, but they have relaxed isolation properties to share the Operating System (OS) among the applications. Therefore, containers are considered lightweight. Similar to a VM, a container has its own filesystem, share of CPU, memory, process space, and more. As they are decoupled from the underlying infrastructure, they are portable across clouds and OS distributions.
>
> 
Containers have become popular because they provide extra benefits, such as:
> - Agile application creation and deployment: increased ease and efficiency of container image creation compared to VM image use.
> - Continuous development, integration, and deployment: provides for reliable and frequent container image build and deployment with quick and efficient rollbacks (due to image immutability).
> - Dev and Ops separation of concerns: create application container images at build/release time rather than deployment time, thereby decoupling applications from infrastructure.
> - Observability: not only surfaces OS-level information and metrics, but also application health and other signals.
> - Environmental consistency across development, testing, and production: Runs the same on a laptop as it does in the cloud.
> - Cloud and OS distribution portability: Runs on Ubuntu, RHEL, CoreOS, on-premises, on major public clouds, and anywhere else.
> - Application-centric management: Raises the level of abstraction from running an OS on virtual hardware to running an application on an OS using logical resources.
> - Loosely coupled, distributed, elastic, liberated micro-services: applications are broken into smaller, independent pieces and can be deployed and managed dynamically – not a monolithic stack running on one big single-purpose machine.
> - Resource isolation: predictable application performance.
> - Resource utilization: high efficiency and density.


## What is Container Platform – Docker?
> In containerization a developer packages the application along with all its dependencies and libraries and the entire environment in a box that we call container, and this can be then shipped using a container platform like docker and that can be deployed on different systems and platforms.
> Container orchestration tool like Kubernetes can manage – 
Deploying, Scaling Up/Down, Scheduling, load balancing, batch execution of processes, rollbacks, monitoring
>
> At the core Docker helps to start/stop/delete the containers which is a lower level management whereas Kubernetes does higher level of management like how many containers to run, on which node to run them, scaling them up or down
Lets say we have an application where there are 2 nodes for frontend and one node for backend, When the load on frontend increases or if a node goes down the master node will produce more nodes for front end and when demand decreases it will destroy those nodes  


## Kubernetes Features

Kubernetes has many features that help orchestrate containers across multiple hosts, automate the management of K8s clusters, and maximize resource usage through better utilization of infrastructure. Important features include:

> - Auto-scaling. Automatically scale containerized applications and their resources up or down based on usage. Define complex containerised applications and deploy them across a cluster of servers or even multiple clusters with Kubernetes. As Kubernetes scales applications according to your desired state, it automatically monitors and maintains container health.

> - Lifecycle management. Automate deployments and updates with the ability to:
o	Rollback to previous versions
o	Pause and continue a deployment

> - Declarative model. Declare the desired state, and K8s works in the background to maintain that state and recover from any failures.

> - Resilience and self-healing. Auto placement, auto restart, auto replication and auto scaling provide application self-healing Build more extensible apps

> - A large open-source community of developers and companies actively builds extensions and plugins that add capabilities such as security, monitoring and management to Kubernetes. Plus, the Certified Kubernetes Conformance Program requires every Kubernetes version to support APIs that make it easier to use those community offerings.

> - Persistent storage. Ability to mount and add storage dynamically

> - Load balancing. Kubernetes supports a variety of internal and external load balancing options to address diverse needs

> - DevSecOps support. DevSecOps is an advanced approach to security that simplifies and automates container operations across clouds, integrates security throughout the container lifecycle, and enables teams to deliver secure, high-quality software more quickly. Combining DevSecOps practices and Kubernetes improves developer productivity.

> - Make workloads portable - Because container apps are separate from their infrastructure, they become portable when you run them on Kubernetes. Move them from local machines to production among on-premises, hybrid and multiple cloud environments—all while maintaining consistency across environments.

> - Service discovery and load balancing Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.

> - Storage orchestration Kubernetes allows you to automatically mount a storage system of your choice, such as local storages, public cloud providers, and more.

> - Automated rollouts and rollbacks You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.

> - Automatic bin packing You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.

> - Self-healing Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.

> - Secret and configuration management Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.

> - Storage Orchestration - Containers running inside a pod may need to store data. PODs can have a storage volume.
Usually there is a single volume which is shared within all the containers in a pod.
Kubernetes allows to mount the storage system of your choice like -local, cloud AWS, network nfs,

> - Self Healing - If a Container fails – K8s will restart the container
If a node dies – K8s will replace and reschedule containers of that node on any other available node. 
K8s has a monitoring system, - If container does not respond to monitoring checks or user defined health checks – it will kill the container and take care of availability of application. The process which take care of all these is called Replication-Controller.

> - Automated rollouts and Rollbacks
Rollouts – deploy changes to the application or its configuration
Rollbacks – revert the changes and restore to previous state
Kubernetes progressively rolls out changes to your application or its configuration, while monitoring application health to ensure it doesn’t kill all your instances at the same time. If something goes wrong, Kubernetes will rollback the changes for you. It also ensures there is no application downtime during this process.

> - Secret and Config Map - In Kubernetes, passwords, keys, tokens are handled using Secret
Secret is a Kubernetes object and it is created outside pods and containers. Makes sensitive data portable and easy to manage.
In Kubernetes, configurations are handled using Config Maps. Config Maps is a Kubernetes object and it is created outside pods and containers. Makes configuration data portable and easy to manage.
Secrets and Configurations are stored in ETCD, ETCD is a key value data store(database)

> - Batch Executions - Batch jobs require an executable/process to be run to completion.
In Kubernetes run to completion jobs are primarily used for batch processing.
Each job creates one or more pods.
During job execution if any container or pod fails, job controller will reschedule the container, pods on another node.
Can run multiple pods in parallel and scale up if required.
After job is completed, the pods will move from running state to shut down state.





## Components of Kubernetes

> - Ingress – The request we make from browser first goes to ingress and ingress then forwards it to Service.
https://myapp.com    is the ingress and ingress reroutes it to http://124.89.10.12:8080 which is basically a service.

> - ConfigMap – Its an external configuration of the application.
It contains configuration data of urls of database or some other services we use.

> - Secret – Secret is same as configMap but it is used to store secret data like db username and db password or other credentials. Data is not stored in plain text format but in base64 encoded

> - Volumes – It attaches physical storage on harddrive to your pod to the local hardrive or cloud storage or other VM etc
Kubernetes/k8s cluster is not responsible for managing the data and storing it persistently. We as an administrator are responsible for managing and storing and replicating the data.

> - Deployment – Blueprint of our pod is known as Deployments. In practice we don’t create pods, we have to create deployments and in this way we can scalu up or scale down based on our requirement.
Since pod is a layer of abstraction on top of containers, here deployment is another layer of abstraction on top of pods

Stateless and Stateful
> - StatefulSet – Deployment is only used to create stateless apps where as for statefull thing like databases there is another Kubernetes component  which is used to create and manage it which is StatefullSet.
StatefulSet just like Deployment take care of replicating the PODS and scaling them up or down but making sure that database reads and writes are synchronized so that there are no db inconsistencies left
Stateless is when it does not store or preserve any data or its state like eg: the App or front end
Stateless doesn’t have to remember stuff
Stateful is when it preserves its state or stores data and maintains data consistency eg: Database or backend
Stateful has to remember stuff




















https://github.com/nigelpoulton/getting-started-k8s
