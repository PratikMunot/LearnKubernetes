```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ngin

```

### Labels and Selectors

The way connection is established is via Labels and Selectors 
Metadata part contains the labels and spec part contains selectors. Each component like a deployment or pod etc can be given a label ie a key value pair. Each and every pod created via this deployment will be given the label mentioned in that metadata section of deployment in other words Pods get the label through the template blueprint. Now if there is some other component like say service and if it has to connect with pods of deployment, it needs to know which pods to connect to so service will match the labels from its selector section for this. 


### Ports in Service and Pod

The service yaml file will have spec which contains ports section. In the ports section there are 2 fields port and targetPort. 
The port is where service itself will listen to and service itself accepts the requests and targetPort is the port where service will forward the request to pod. That means its the port of pod which is listening the request will be sent to that port number of pod. targetPort in service will be matched to the containerPort in deployment. 
Example - If DB Service sends a request to nginx service it has to send the request on port 80 and then the nginx service will send the request to targetPort 8080 which matches with the conatiner port 8080. The pod was listening on port 8080 
