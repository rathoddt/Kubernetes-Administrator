# Stoage
Configure a volume to store these logs at /var/log/webapp on the host.
Use the spec provided below.
    - Name: webapp
    - Image Name: kodekloud/event-simulator
    - Volume HostPath: /var/log/webapp
    - Volume Mount: /log

<code>
  - env:    
    volumeMounts:
    - mountPath: /log
      name: log-volume
... 
  volumes:
  - name: log-volume
    hostPath:
      path: /var/log/webapp
</code>
  

`/tmp/kubectl-edit-2935622297.yaml`  


Create a Persistent Volume with the given specification.
    - Volume Name: pv-log
    - Storage: 100Mi
    - Access Modes: ReadWriteMany
    - Host Path: /pv/log
    - Reclaim Policy: Retain


`kubectl create -f pv.yaml` 
`kubectl get pv`  

Claim some of that storage for our application. Create a Persistent Volume Claim with the given specification.

`kubectl create -f pvc.yaml`  
`kubectl get pvc`  

Update the Access Mode on the claim to bind it to the PV.

Delete and recreate the claim-log-1.
   -  Volume Name: claim-log-1
   -  Storage Request: 50Mi
   -  PVol: pv-log
   -  Status: Bound

`kubectl replace --force -f pvc.yaml `  