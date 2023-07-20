

# Cluster Networking
What is the IP address of the Default Gateway? <br>
`ip route`  
look for row with defualt value

On what port kube-scheduler is listening on
<code>
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