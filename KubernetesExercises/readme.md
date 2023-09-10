
### 1.1 Create a simple Nginx deployment
Lets create a simple deployment of nginx image with name nginx-depl
```
Syntax - kubectl create deployment <deployment-name> --image=<image-name>
#  kubectl create deployment nginx-depl --image=nginx
deployment.apps/nginx-depl created
```
Verify if deployment created successfully
```
  
# kubectl get pod
NAME                         READY   STATUS    RESTARTS   AGE
nginx-depl-56cb8b6d7-6w9nb   1/1     Running   0          35s

# kubectl get deployments
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
nginx-depl   1/1     1            1           39s
```

### 1.2 Edit the Deployment
```
kubectl edit deployment <deployment-name>
edit the changes you want like changing image or image version and then save the file
To check if its working fine do following. The age of pod/deplyment would have been changed
kubectl get pod
kubectl get deployment 
```

`kubectl get deployments`

``kubectl get deployments``
