# Stoage
Configure a volume to store these logs at /var/log/webapp on the host.

<code>
  - env:    
    volumeMounts:
    - mountPath: /log
      name: log-mount

. . . 
  volumes:
  - name: log-volume
    hostPath: 
      path: /var/log/webapp
</code>

`kubectl create -f pv.yaml` 

Claim some of that storage for our application. Create a Persistent Volume Claim with the given specification.

`kubectl create -f pvc.yaml`  