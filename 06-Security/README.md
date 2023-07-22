# Security

<code>
ls /etc/kubernetes/manifests/
cat /etc/kubernetes/manifests/kube-apiserver.yaml 
cat /etc/kubernetes/manifests/etcd.yaml   
</code>

What is the Common Name (CN) configured on the Kube API Server Certificate?

OpenSSL Syntax: `openssl x509 -in file-path.crt -text -noout`  

`openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout`  

### Issue 1
Kubectl suddenly stops responding to your commands. Check it out! Someone recently modified the `/etc/kubernetes/manifests/etcd.yaml` file

You are asked to investigate and fix the issue. Once you fix the issue wait for sometime for kubectl to respond. Check the logs of the ETCD container.
<code>
docker ps -a | grep kube-apiserver
docker logs <api-server-container-id>
docker ps -a | grep etcd

ls /etc/kubernetes/pki/
ls /etc/kubernetes/pki/etcd/
cat /etc/kubernetes/manifests/etcd.yaml | grep server-certificate.crt
vim /etc/kubernetes/manifests/etcd.yaml
// use crictl if neccessary
k get pods
crictl ps -a
crictl ps -a | grep kube-apiserver
crictl logs c68467a2a709e  
crictl ps -a | grep kube-apiserver
</code>

### Issue 2
The kube-api server stopped again! Check it out. Inspect the kube-api server logs and identify the root cause and fix the issue.

Run crictl ps -a command to identify the kube-api server container. Run crictl logs container-id command to view the logs.
<code>
crictl ps -a | grep kube-apiserver
crictl logs 6227bd60d3e4b
ls /etc/kubernetes/manifests/
cat /etc/kubernetes/manifests/kube-apiserver.yaml 
crictl ps -a | grep etcd
crictl logs 919b3dde6fa6b
k get nodes
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep etcd
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep "\-\-etcd"
cat /etc/kubernetes/manifests/kube-apiserver.yaml 
crictl ps -a | grep kube-apiserver
k get pods
</code>

### Certificate API
<code>
ls /root
cat akshay.csr 
cat akshay.key 
cat akshay.yaml
cat > akshay.yaml
cat  akshay.yaml
cat akshay.csr | base64
cat akshay.csr | base64 -w 0
vim akshay.yaml 
k create -f akshay.yaml 
k get csr
k certificate approve akshay
k get csr
k get csr agent-smith -o yaml
k certificate deny agent-smith
k delete csr agent-smith
</code>

### kubeconfig
<code>
ls -a
ls .kube/
cat .kube/config 
ls
cat my-kube-config 
kubectl config use-context research --kubeconfig /root/my-kube-config
cat my-kube-config 
mv /root/my-kube-config /root/.kube
mv /root/my-kube-config /root/.kube/config
ls
ls /root/.kube/
rm /root/.kube/config 
mv /root/.kube/my-kube-config /root/.kube/config
k get nodes
ls /etc/kubernetes/pki/
kubectl config view
ls /etc/kubernetes/pki/
ls /etc/kubernetes/pki/users/
ls /etc/kubernetes/pki/users/dev-user/
vim /root/.kube/config 
k get nodes
</code>

### RBAC
k get roles
ls /etc/kubernetes/pki/
ls /etc/kubernetes/manifests/
cat /etc/kubernetes/manifests/kube-apiserver.yaml 
k get roles
k get roles -A
k get roles -A | wc -l
k describe role kube-proxy  -n kube-system
d get rolebindings kube-system
d get rolebindings -n kube-system
k get rolebinding -n kube-system
k describe rolebinding -n kube-system
k describe rolebinding kube-prox -n kube-system
cat /root/.kube/config
k auth can-i get pods  --as dev-user
cat > dev-userr-role.yaml
vim dev-userr-role.yaml 
vim rb-dev-user.yaml
vim dev-userr-role.yaml 
vim rb-dev-user.yaml
crictl ps aux | grep authorization
crictl ps aux | grep author
crictl ps -aux | grep authorization
crictl ps -aux | grep autho
crictl ps
crictl ps -aux
crictl ps -aux | grep auth
ps -aux | grep auth
k config view
k get pods --as dev-user




### Issue 3
Create the necessary roles and role bindings required for the dev-user to create, list and delete pods in the default namespace.

<code>
k create -f dev-userr-role.yaml 
k create -f rb-dev-user.yaml 
k delete role.rbac.authorization.k8s.io/developer 
cat dev-userr-role.yaml 
k create role developer --verb=list,create,delete resources=pods
k get roles
k create role developer --verb=list,create,delete resource=pods
kubectl create role -h'
kubectl create role -h
k create role developer --verb=list,create,delete --resource=pods
k describe role developer
k get rb
k get rolebinding
k delete rolebinding dev-user-binding
k create rolebinding dev-user-binding --role=developer --user=dev-user
k describe rolebinding dev-user-binding 
</code>

### Issue 4
A set of new roles and role-bindings are created in the blue namespace for the dev-user. However, the dev-user is unable to get details of the dark-blue-app pod in the blue namespace. Investigate and fix the issue.

We have created the required roles and rolebindings, but something seems to be wrong.

<code>
k get pod dark-blue-app -n blue --as dev-user
k get role -n blue
k get rolebinding -n blue
k describe  rolebinding -n blue
k describe role -n blue
k edit rolebinding dev-user-binding -n blue
k edit role devloper -n blue
k edit role developer -n blue
k describe role developer -n blue
k edit role developer -n blue
</code>