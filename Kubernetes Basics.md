
Kubernetes Basics

Before knowing Kubernetes we should understand about containers and Docker.

**Container: Introduction**

In real world it advanced from (Physical servers --> VM--> Containers)
 
  Hypervisor is a virtualization platform thats creates and manages(basically seperates and creates indvidually as per snippet below) applications and its OS- each application has its own OS and highly secure and it is Good.

<img width="301" height="225" alt="Image" src="https://github.com/user-attachments/assets/146f0b2e-82b0-49f4-a923-ed292eb5e295" />


But it can be like we are not using complete resources- for example if an organization bought 1000 GB phyiscal server and installed Hypervisor and it is 
divided into different VM but the organization will not use complete resources.

So we should now understand, why we moved to containers-- same thing as above we are not using full capacity of the resources as some apps need only less resources even though they are running on full fledged mode, like it can only use 20 or 30 GB even though the VM has 100 GB space. so here we are wasting some resources.

So containerization will solve some problems of virtualization - not all as Virtualization is more secured when compared to containerization because they are strictly isolated where as container can talk to other containers and there will be some sort of leakage.

Containerzation can be done in two ways:

1- it can be done on top of physical server.
2- it can be done on top of VM or EC2 -- this is through some cloud provider and most commonly used as there wont be any additional maintainence or adminstrator required.

<img width="712" height="441" alt="Image" src="https://github.com/user-attachments/assets/8698c22b-94ea-4d6d-a741-95e25f01bfd9" />


Docker:  

Docker images are very light weight reasons:
- No full OS for each container- uses OS from base image OS
- It packages app and its depndencies and share the common Host
- makes it easy to ship(deploy)
  
**Life cycle of Docker container.**

write some commands and create docker file--> create Docker image and also run the container --> push to Docker registory----------> from Docker registory--> we can again pull the image and run the container

Docker engine is playing a role in creating and running an image and container-- we use build and run commands.




## Kubernetes ##

**Diff between Docker and K8s**

K8s- Orchestration platform -just a text book def from Google

we need to know more and why K8s is being used if containers are solving the problem of virtualization

Containers are ephemeral- means short lived - die or revive any time

**Problem 1** - if there are some 10 containers running on one Docker image- and if one container is consuming more resources and it is not giving enough resources for other container or blocking other container creation-- **means single host problem** in docker.
**Problem 2** - If any container get killed by any reason - there is **no auto healing** in docker.
**Problem 3** - On demand basis or on high load- there is **no auto scaling** in docker. Load balancer will support auto scaling
**Problem 4**- no enterprise level suport like load balance, fire wall, auto scale, auto heal, API gateway. as it is simple and minimilistic.

K8s solves above 4 problems.

**Cluster(group of nodes)**- means k8s installed in Master/Node architecture- **It solves problem 1** -- as k8s is by default cluster based and it has mutiple nodes, if it finds a faulty node it moves it to different node.
 In each node there will be n number of containers means pods means apps :) --- so if one container has a problem in one node, it moves to different node.

**API Server**- if receives any signal of any problem- it creates new container.- **auto healing**

**Replica sets** - used to increase the nodes based on demand - **auto scaling**.

K8s is from Google and part of Borg 
they built enterprise level solution, Docker cannot be used in production as it doesnt support **enterprise level solution alone**.

K8s solves this problem but not 100 % but is its evolving, VMs are far secured than K8s and Docker

CNCF organization is continuously working on evolving K8s for ex- Ingress contrllers were advanced thing to solve load balancer cooncept in k8s


## K8s architecture ##

<img width="832" height="507" alt="Image" src="https://github.com/user-attachments/assets/bbc1d769-f02a-46e0-8081-d78ba69ff191" />


To understand in better way we will compare with Docker and learn the architecture and its components. so it makes sense



| Docker | Kubernetes |  
|:-----  |:------:    |
| **Container run time component**: Docker has Docker shim which is needed for running container   |   **Kublet** which is responsible for maintaining the pod running in K8s(inform if there is any problem when pod is not running it basically make sures od is running all the tie if not informs other component).**Container run time** in K8s actually runs the pod, also K8 supports other components like Docker shim, containerd, crio-o  | 
| **Networking** : Docker-0 bridge networking is mandatory for running pod   | **Kube-proxy**- responsible for networking like allocating ip address and default load balancing capabilities for k8s | 


Master Node components:

| Components | Description |  
|:-----  |:------:    |
| **API server/control plane**    |  Core component of K8s, it takes requests from external world    |  
|**Scheduler**| responsible for scheduling resources in K8s, recieves info from API server based on that it will create pod on respective nodes     | 
| **etcd**    | backup service- creates Key value pair, helps in restoring cluster call'd as Key value store     | 
|**controller manager**    | controllers for auto scalling- replica set in K8s is a type of controller in K8s file if it is mentioned as 2 pods it will make sure 2 pods are always running and controller manager takes care controllers, will check if they are running or not      | 
|**Cloud controller manager-CCM**    | If K8s has to create any storage or resource on any cloud service, it has to translate the request and sends to API which the cloud provider understands, this mechanism has to be implemneted on CCM     | 

**so basically master node components, controls the actions- and worker node components does the actions.**

























