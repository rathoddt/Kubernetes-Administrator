# Application Lifecycle Management

`kubectl describe deployment.apps/frontend`  


`kubectl get all`  
`kubectl get pods --watch`  

`kubectl get pods`  
`alias`  
`bash /root/curl-test.sh`  
`kubectl edit deployment frontend`  


Upgrade the application by setting the image on the deployment to `kodekloud/webapp-color:v3`   

`k set image deploy frontend simple-webapp=kodekloud/webapp-color:v3`  

## Configure Applications
Configuring applications comprises of understanding the following concepts:

- Configuring Command and Arguments on applications
- Configuring Environment Variables
- Configuring Secrets




Unlike virtual machines, containers are not meant to host an operating system.

Containers are meant to
- run a specific task
- or process, such as to host an instance of a web server or application server or a database,
- or simply to carry out some computation or analysis.


Once the task is complete, the container exits.


How do you specify a command to start the container?

One option is to append a command to the Docker run command
and that way, it overrides the default command specified
within the image.


But how do you make that change permanent?
Say you want the image to always run the sleep command
when it starts.

You would then create your own image
from the base Ubuntu image
and specify a new command.

I could now simply run the Docker Ubuntu sleeper command
and get the same results.


The entry point instruction is like the command instruction,
as in, you can specify the program
that will be run when the container starts.


So that's the difference between the two.
In case of the CMD instruction,
the command line parameters passed
will get replaced entirely.

Whereas in case of entry point,
the command line parameters will get appended.


There are two fields (in pod definition file) that correspond 
to two instructions in the docker file.

The command field overrides the entry point instruction,
and the args field overrides the command instruction
in the docker file.



`k get pod webapp-color  -o yaml > greep-app.yaml`  

`k create -f greep-app.yaml `  
`k get po`  
`k get configmap`  
`k describe db-config`  
`k describe configmap db-config`  

`k get cm`  
`k describe cm webapp-color `  
`k delete cm webapp-color `  

`kubectl create configmap webapp-config-map --from-literal=APP_COLOR=darkblue --from-literal=APP_OTHER=disregard`  


`kubectl replace --force -f /tmp/kubectl-edit-2631806284.yaml`  
`k get cm`  