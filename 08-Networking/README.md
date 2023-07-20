

What is the IP address of the Default Gateway?
`ip route`  
look for row with defualt value

O what port kube-scheduler is listening on
<code>
netstat --help
ps aux
netstat -l
netstat -l | grep -i scheduler
netstat -npl | grep -i scheduler
</code>