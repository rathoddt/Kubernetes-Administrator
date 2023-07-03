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

`kubectl create –f replicaset-definition.yml`  
`kubectl get replicaset`  
`kubectl delete replicaset myapp-replicaset`   *Also deletes all underlying PODs
`kubectl replace -f replicaset-definition.yml`  
`kubectl scale –replicas=6 -f replicaset-definition.yml`  



    1  kubctl get pods
    2  kubectl get pods
    3  kubectl get rc
    4  kubectl get rc
    5  kubectl get replicaset
    6  kubectl get pods
    7  kubectl describe pod new-replica-set-75x9w
    8  kubectl delete pod busybox777
    9  kubectl delete pod new-replica-set-75x9w 
   10  kubectl get pods
   11  clear
   12  pwd
   13  ls
   14  kubectl create -f replicaset-definition-1.yaml
   15  vim replicaset-definition-1.yaml
   16  kubectl create -f replicaset-definition-1.yaml
   17  ls
   18  kubectl create -f replicaset-definition-2.yaml
   19  vim replicaset-definition-2.yaml
   20  vim replicaset-definition-2.yaml
   21  kubectl create -f replicaset-definition-2.yaml
   22  kubectl get replicasets
   23  kubectl delete replicaset replicaset-1
   24  kubectl delete replicaset replicaset-2
   25  kubectl get replicasets
