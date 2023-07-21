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