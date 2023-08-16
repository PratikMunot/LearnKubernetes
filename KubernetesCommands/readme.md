

### Verify Installation
```
# minikube version
# kubectl version
# docker version

Minikube – is for start-up/creating or deleting the cluster
Kubectl is for managing and configuring the Minikube cluster and its nodes
```


Start minikube (Start the Cluster)
```
# minikube start
OR
#  minikube start --driver=docker
OR
#  minikube start --driver=virtualbox
OR
# if we are using a VM then use this cmd
# minikube start --driver=none
```


Cluster Status
```
# minikube status
```


# PODS
Get details of Pods / Display all pods
```
# kubectl get pod
# kubectl get pod -o wide
# kubectl get pod -o yaml 
# kubectl get pod -o json
```

Display all available info and details of Pod
```
# kubectl describe pod                                # describes all pods
# kubectl describe pod <pod-name>           # describes specific pod
```

Delete a Pod 
```
# kubectl delete pod <pod-name>
```

Display logs of pod 
```
# kubectl logs <pod-name>
```

Get inside the Pod/container for troubleshooting
```
# kubectl exec -it <pod-name> -- bin/bash
# exit - to exit out of container
```



# Replicaset
Get replica-set details  - Replicaset is managing the replicas of pod. We don’t have to manage replicaset directly, we just need to work with deployment to specify how many replicaset we want

```
# kubectl get replicaset
# kubectl get replicaset -o wide
# kubectl get replicaset -o yaml
# kubectl get replicaset -o json
```


Display all available info and details of Replicaset
```
# kubectl describe replicaset                                         # describes all RS
# kubectl describe replicaset <replicaset-name>                       # describes specific RS

```


# Deployment
Get Deployment details
```
# kubectl get deployment
# kubectl get deployment -o wide
# kubectl get deployment -o yaml
# kubectl get deployment -o json

```

Display all available info and details of Deployment
```
# kubectl describe deployment                                             # describes all deployment
# kubectl describe deployment <deployment-name>           # describes specific deployment
```


### Creating Deployment

Pod is the smallest unit, but we are not going to create POD. We will be creating Deployment instead which is an abstraction over Pods. Deployment is a blueprint for creating pods. The most basic configuration for deployment is (name and image to use as shown below)
Between deployment and pod there is another layer which is automatically managed by k8s deployment which is replica-set
Syntax – 
```
# kubectl create deployment <Deployment-NAME> --image=<image-name> [--dry-run=server|client|none] [options]
```
Eg- this will create a deployment and download latest image of nginx from docker hub
```
# kubectl create deployment nginx-depl --image=nginx 
```

Edit Deployment
```
# kubectl edit deployment <deployment-name>
```
An auto generated deployment file which is created when we create a deployment, and it is opened and we can make changes to deployment here (all values are default). As soon as we make changes here and save it, Kubernetes will try to update the changes in the cluster. If we change image in deployment and save changes and check for pod or replicaset detail, then we see old pod is terminated and new pod is created


Delete Deployment 

This will delete all the Pods and replicaset under that deployment
```
# kubectl delete deployment <deployment-name>
```

# Kubernetes Configuration file

> Every Configuration file in Kubernetes has 3 parts
> - metadata – First part is the where the metadata of the component that you are creating resides
> - spec – Specification – Each components configuration file will have specification where we put every kind of specification or configuration that you want to apply for that component. Attributes under spec will be different based on each kind of component that we are trying to create
> - status – Status will be automatically generated and added by Kubernetes. In this part Kubernetes will add the current status of the com ponent. The way it works is – Kubernetes will always come here to check and match what is the desired state mentioned in spec part and what is the current state in the status part. If both doesn’t match then it knows something needs to be fixed so it tries to do self healing.

> Kubernetes gets the current status data of component from etcd. Etcd is the brain of the cluster and it holds the current status of any k8s components
> The first 2 lines are – 
> - apiVersion – is different for different components
> - kind – what kind of component we are creating

> Sometime a Deployment will have template and that template will have its own metadata and spec section. This metadata applies to a pod and acts as a blueprint for POD

> The way the connections are established is through labels and selectors
> Metadata section contains labels and spec section contains selector
> Service will contain selector and other components like deployment or pod will contain label. In this way service will know which pods are under it
  

> Targetport in service should match container port. Service has its own port where we can connect to it











