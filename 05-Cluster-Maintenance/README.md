# Cluster maintenance

## OS Upgrade
We need to take `node01` out for maintenance. Empty the node of all applications and mark it unschedulable.
`kubectl get nodes`  
`kubectl get pods`  


`kubectl drain node01`  
`kubectl get pods -o wide`  

`alias`  
`alias k=kubectl`  

`kubectl drain node01 --ignore-daemonsets`  

`kubectl get all -o wide`  


`kubectl uncordon node01`  
`k get nodes`  
`kubectl get pods -o wide`  

`kubectl get rs`  
`kubectl get all`  
`k cordon node01`  

