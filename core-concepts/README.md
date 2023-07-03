# Kubernetes-Administrator

Hetting help for a command
`kubectl run --help`  

`kubectl run nginx --image nginx`  
`kubectl get pods`  

`kubectl get pods`  
`kubectl describe pod  newpods-wszjv`  
`kubectl get pods`  
   
Finding on which node pods are running

`kubectl get pods -o wide`
`kubectl delete pod webapp`

Create a new pod with name `redis` and with image `redis123`
Use pod-definition YAML file

`kubectl run redis --image=redis123 --dry-run=client -o yaml`  
Output
`apiVersion: v1`  
kind: Pod  
metadata:  
  creationTimestamp: null  
  labels:  
    run: redis  
  name: redis  
spec:  
  containers:  
  - image: redis123  
    name: redis  
    resources: {}  
  dnsPolicy: ClusterFirst  
  restartPolicy: Always  
`status: {}`

` kubectl run redis --image=redis123 --dry-run=client -o yaml > redis.yaml`  
`kubectl create -f redis.yaml`  
`kubectl apply -f redis.yaml`


`Replcation Controller` is replaced by `Replica Set` - new way of doing thing
