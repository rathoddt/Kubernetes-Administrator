# Scheduling
## Manul Scheduling
`kubectl apply -f nginx.yaml `  
`kubectl get po`  
`kubectl describe pod nginx`  
`kubectl delete pod nginx`  
`kubectl create pod --help`

`vim nginx.yaml`   
`kubectl  get cs`

`kubectl get nodes`
`kubectl get pods -n kube-system`
`vim nginx.yaml `
`kubectl create -f nginx.yaml `

`kubectl create -f nginx.yaml`   
`vim nginx.yaml `  
`kubectl delete pod nginx`

`vim nginx.yaml`   
`kubectl replace --force -f nginx.yaml`  

## Labels and selectors
`kubectl get ns`  
`kubectl get all`  
`kubectl get pods -A`  

`kubectl get pods --selector env=dev`  
`kubectl get pods --selector bu=finance`  
`kubectl get all --selector env=prod`  

`kubectl get all --selector env=prod --no-headers`  
`kubectl get all --selector env=prod --no-headers | wc -l`  

`kubectl get all --selector env=prod,tier=frontend,bu=finance`  


`kubectl create -f replicaset-definition-1.yaml `  
`vim replicaset-definition-1.yaml `

`kubectl create -f replicaset-definition-1.yaml `  

## Node afinity

Apply a label color=blue to node node01
`kubectl label node node01 color=blue`  

Create a new deployment named blue with the nginx image and 3 replicas.
 `kubectl create deployment blue --image=nginx --replicas=3`  

Which nodes can the pods for the blue deployment be placed on?

`kubectl get nodes`