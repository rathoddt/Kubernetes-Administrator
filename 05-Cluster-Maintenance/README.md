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


## Cluster upgrade
Upgrade the `controlplane` components to exact version v1.27.0

Upgrade the kubeadm tool (if not already), then the controlplane components, and finally the kubelet. Practice referring to the Kubernetes documentation page.
https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/

`k get nodes`  
`k get pods -A | wc -l`  
`k describe node controlplane`  

`k get pods -o wide`  


`k describe node | grep -i taints`  

`kubeadm upgrade plan`  

`kubectl drain controlplane --ignore-daemonsets`  


`cat /etc/os-release`   
`cat /etc/*release*`  

`apt update`  
`apt-cache madison kubeadm`
`apt-mark unhold kubeadm && apt-get update && apt-get install -y kubeadm=1.27.0-00 && apt-mark hold kubeadm`   

`kubeadm version`   
`kubeadm upgrade plan`   

`sudo kubeadm upgrade apply v1.27.0`   
`apt-mark unhold kubelet kubectl && apt-get update && apt-get install -y kubelet=1.27.0-00 kubectl=1.27.0-00 && apt-mark hold kubelet kubectl`   

`sudo systemctl daemon-reload`   
`sudo systemctl restart kubelet`   

`kubectl get nodes`   
`kubectl uncordon controlplane`   



`k drain node01 --ignore-daemonsets `   


`ssh node01`  

These two commands after uprading worker node  
`k uncordon node01`   
`k get nodes` 




Upgrade the worker node to the exact version v1.27.0
https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/upgrading-linux-nodes/

`cat /etc/*release*` 

replace x in 1.27.x-00 with the latest patch version
`apt-mark unhold kubeadm && \`
`apt-get update && apt-get install -y kubeadm=1.27.0-00 && \`
`apt-mark hold kubeadm` 

`sudo kubeadm upgrade node`   

replace x in 1.27.x-00 with the latest patch version
`apt-mark unhold kubelet kubectl && \`
`apt-get update && apt-get install -y kubelet=1.27.0-00 kubectl=1.27.0-00 && \`
`apt-mark hold kubelet kubectl`    

`sudo systemctl daemon-reload`   
`sudo systemctl restart kubelet`   







