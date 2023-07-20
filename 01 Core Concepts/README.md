# Kubernetes-Administrator

Hetting help for a command
`kubectl run --help`  

`kubectl run nginx --image nginx`  
`kubectl get pods`  

`kubectl describe pod  newpods-wszjv`  
   
Finding on which node pods are running

`kubectl get pods -o wide`  
`kubectl delete pod webapp`

Create a new pod with name `redis` and with image `redis123`
Use pod-definition YAML file

` kubectl run redis --image=redis123 --dry-run=client -o yaml > redis.yaml`  
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


`kubectl create -f redis.yaml`  
`kubectl apply -f redis.yaml`


`Replcation Controller` is replaced by `Replica Set` - new way of doing thing

`kubectl create –f replicaset-definition.yml`  
`kubectl get replicaset`  
`kubectl delete replicaset myapp-replicaset`   *Also deletes all underlying PODs
`kubectl replace -f replicaset-definition.yml`  
`kubectl scale –replicas=6 -f replicaset-definition.yml`  

`kubectl get rc`  
`kubectl get replicaset`  

`kubectl describe pod new-replica-set-75x9w`  
`kubectl delete pod busybox777`  

`kubectl create -f replicaset-definition-1.yaml`  

`kubectl create -f replicaset-definition-2.yaml`  
`kubectl get replicasets`  
`kubectl delete replicaset replicaset-1`  
`kubectl edit replicaset new-replica-set`  
`kubectl scale --replicas=5 replicaset new-replica-set`  
 `kubectl scale --replicas=2 replicaset new-replica-set`  


   ## Deployments
   While you would be working mostly the declarative way - using definition files, imperative commands can help in getting one time tasks done quickly, as well as generate a definition template easily. This would help save considerable amount of time during your exams.

Before we begin, familiarize with the two options that can come in handy while working with the below commands:

`--dry-run`: By default as soon as the command is run, the resource will be created. If you simply want to test your command , use the --dry-run=client option. This will not create the resource, instead, tell you whether the resource can be created and if your command is right.

`-o yaml`: This will output the resource definition in YAML format on screen.

   Create an NGINX Pod

`kubectl run nginx --image=nginx`  

Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)  

`kubectl run nginx --image=nginx --dry-run=client -o yaml`

Create a deployment

`kubectl create deployment --image=nginx nginx`

Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)

`kubectl create deployment --image=nginx nginx --dry-run=client -o yaml`

Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run) and save it to a file.

`kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml`  

Make necessary changes to the file (for example, adding more replicas) and then create the deployment.

`kubectl create -f nginx-deployment.yaml`  
OR

In k8s version 1.19+, we can specify the --replicas option to create a deployment with 4 replicas.

`kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml`

## Services
`kubectl describe svc kubernetes`

`kubectl get svc`  
`kubectl get all`  
`kubectl describe svc kubernetes`  
`kubectl describe deploy simple-webapp-deployment | grep -i image`    
`kubectl create -f service-definition-1.yaml`  

`kubectl delete service webpp-service`  


Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379

`kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml`

(This will automatically use the pod's labels as selectors)

Or

`kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml` 

(This will not use the pods labels as selectors, instead it will assume selectors as `app=redis`. You cannot pass in selectors as an option. So it does not work very well if your pod has a different label set. So generate the file and modify the selectors before creating the service)



Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes:

`kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml`

(This will automatically use the pod's labels as selectors, but you cannot specify the node port. You have to generate a definition file and then add the node port in manually before creating the service with the pod.)

Or

`kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml`

(This will not use the pods labels as selectors)

Both the above commands have their own challenges. While one of it cannot accept a selector the other cannot accept a node port. I would recommend going with the kubectl expose command. If you need to specify a node port, generate a definition file using the same command and manually input the nodeport before creating the service.

## Namespaces
`kubectl get ns`  
`kubectl get ns | wc -l`  
`kubectl get all -n research`  

`kubectl run --image=nginx nginx -n finance`  
`kubectl run --image=redis redis -n finance`  
`kubectl get pods --all-namespaces`  
`kubectl get pods --all-namespaces | grep blue`  
`kubectl get pods -A | grep blue`  

### Imperative commands
`kubectl run --image=nginx:alpine nginx-pod`  
`kubectl get pod`

`kubectl run --image=redis:alpine redis --labels="tier=db"`

`kubectl expose pod redis --name redis-service --port 6379`

`kubectl create deployment --image=kodekloud/webapp-color --replicas=3 webapp`

`kubectl run custom-nginx --image=nginx --port 8080`  
`kubectl get pods`
`kubectl create namespace dev-ns`

`kubectl create deployment redis-deploy -n dev-ns --replicas=2 --image=redis`

`kubectl run httpd --image=httpd:alpine --port=80 --expose=true`
