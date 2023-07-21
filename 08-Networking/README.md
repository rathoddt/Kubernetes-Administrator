

# Cluster Networking

What is the IP address of the Default Gateway? <br>
`ip route`  
look for row with defualt value

On what port kube-scheduler is listening on
<code>
ip link
ip addr
ip address
netstat --help
ps aux
netstat -l
netstat -l | grep -i scheduler
netstat -npl | grep -i scheduler
</code>

Notice that ETCD is listening on two ports. Which of these have more client connections established?  <br>
<code>
netstat -npa | grep -i etcd 
netstat -npa | grep -i etcd | grep -i 2379 | wc -l
</code>

## CNI
`ps aux | grep -i kubelet | grep -i sock`  
`ps aux | grep -i kubelet | grep -i container-runtime`  

What is the path configured with all binaries of CNI supported plugins

`ls /opt/cni/bin`  

What is the CNI plugin configured to be used on this kubernetes cluster?  
`ls /etc/cni/net.d`  

What binary executable file will be run by kubelet after a container and its associated namespace are created?  
`cat /etc/cni/net.d/10-flannel.conflist `  

### Deploy network solution
Deploy weave-net networking solution to the cluster.   
https://www.weave.works/docs/net/latest/kubernetes/kube-addon/
<code>
k get pods -n kube-system
k describe pod kube-proxy-gmhqs -n kube-system

k describe cm -n kube-system
k describe cm kube-proxy -n kube-system
ls
vim weave-daemonset-k8s.yaml 
kubectl apply -f weave-daemonset-k8s.yaml 
kubectl get pods -n kube-system
</code>