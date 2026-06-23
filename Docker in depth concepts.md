**Multi stage Dockerfile**

# Docker Networking:

Networking allows containers to communicate with each other and with the host system. Containers run isolated from the host system and need a way to communicate with each other and with the host system.

By default, Docker provides two network drivers for you, the bridge and the overlay drivers.



1.Bridge network
2.Host network- insecure
3.overlay network- k8s , swarn
4.Custom bridge network-logical isolation

<img width="1241" height="812" alt="Image" src="https://github.com/user-attachments/assets/409d3bc0-931e-47ec-b46b-e86b08eb2031" />



# Bridge network # 
<img width="673" height="362" alt="Image" src="https://github.com/user-attachments/assets/cbf75dcc-3558-4114-bf4d-fac34f1eec4a" />

**Network commands in Docker:**

docker network ls

NETWORK ID          NAME                DRIVER
xxxxxxxxxxxx        none                null
xxxxxxxxxxxx        host                host
xxxxxxxxxxxx        bridge              bridge

Above snapshot of Bridge network, is the default one- where it creates a private networking with containers and host, allowing containers to communicate with each other and with host system.


and if we want to isolate any container from this private networking and want to create a secure network, then custom bridge network can be created with below command.

**docker network create -d bridge custom_bridge**-- command to create custom bridge

docker network ls

NETWORK ID          NAME                DRIVER
xxxxxxxxxxxx        bridge              bridge
xxxxxxxxxxxx        custom_bridge       bridge
xxxxxxxxxxxx        none                null
xxxxxxxxxxxx        host                host


Now, the newly created network can be attached to a container with below command.


**docker run -d --net=custom_bridge --name db training/postgres**


<img width="902" height="567" alt="Image" src="https://github.com/user-attachments/assets/8593fe8d-4029-4392-a7a7-fb2df3592d73" />


For example: If we have total 3 containers, where two containers are in same network which is default bridge and other one is custom bridge.

so the two containers of default bridhe will be in same subnet and other container will be in different subnet.

we cna check the **ip address** of the containers using inspect command.

**docker inspect <container id>**

Now we will quickly understand host network i docker, which shares the host machine ip.

To attach a **host network** to a Docker container, you can use the --network="host" option when running a docker run command. When you use this option, the container has access to the host's network stack, and shares the host's network namespace. This means that the container will use the same IP address and network configuration as the host.

Here's an example of how to run a Docker container with the host network:

docker run --network="host" <image_name> <command>

Keep in mind that when you use the host network, the container is less isolated from the host system, and has access to all of the host's network resources. This can be a **security risk**, so use the host network with caution.

Not all containers are compatiable with host network.





