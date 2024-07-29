# Docker



LXC old version of container concept new and extended versions is docker which create a virtual environment.

Linux containers can be run in windows but windows containers can’t run on linux

Docker engine of different version of yaml file
Version 1: create a single bridge network where all containers can be reachable
Version 2: Create a separate bridge network where all containers in the yaml file can be reachable not all containers
So, we not need to links containers
Version 3:  All capabilities of Version 2 and much more

The engine consists of three major components:
1.	Docker Daemon: The daemon (dockerd) is a process that keeps running in the background and waits for commands from the client. The daemon is capable of managing various Docker objects.
2.	Docker Client: The client  (docker) is a command-line interface program mostly responsible for transporting commands issued by users.
3.	REST API: The REST API acts as a bridge between the daemon and the client. Any command issued using the client passes through the API to finally reach the daemon.
	


Image (Build an application or OS) [package, template]
Container (Any App or OS which are running in container)



```bash
Some Commands
Docker pull image								[download image from dockerhub]
Docker rmi image								[remove image from the machine]
Docker run -ti (container-name) 						[I = interactive mode]
Docker container ls 								[show running containers]
Docker run -d –name (name) -p (port host:container = 80:8400) image-name			[]
Docker container inspect (image-name or container ID)			[]
Docker exec -ti (container-name or container ID) bash			[interact running container with cli mode]	
Docker exec -ti (container-name or container ID) cat /tmp/file		[run any command without interact container]
Docker run -v /opt/datadir:var/lib/mysql (image-name)			[Data map into host]
Docker run -e (Code which execute) image-name 				[environment variable can be changed if set up ENV in image file]
	
We can interact with any container image with root (docker exec -it cont-ID -u 0 /bin/bash)

 ```


We can use multiple containers with a single image
Creating my own image
We need a dockerfile in linux 

```bash
FROM Ubuntu								[Base ubuntu layer]
RUN apt-get update							[changes in apt packages]
RUN apt-get install python						
RUN pip install flask							[changes in pip packages]
RUN pip install flask-mysql						[changes in pip packages]
COPY . /opt source-code						[Copy code from our host machine]
ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run		[update the entry point with flask command]
```

```bash
Docker build dockerfile -t name/mycustom-app
```




Docker default Network 
Bridge	None	Host
Docker run ubuntu 	Docker run ubuntu –network=none	Docker run ubuntu –network=host
Private internal network
172.17.0.0
Access to container so need to map a port with host machine	Containers are isolated network	Same port will be use for container

Docker engine have embedded DNS we can resolve by container name 
We can change container IP settings by their docker file if image build so we cant changes in image file we again set up new docker file to make any changes.



Docker Volume
Plug volume
Host_dir:Cont_dir
Anonymous volume
:Cont_dir
Name volume
name:Cont_dir
We can change the configuration file in container
Docker volume create data-volume					/var/lib/docker/volume/data-volume
Then we can map volume into container
Docker run -v data-volume:/var/lib/mysql (image-name)
If container will destroy so all data will be saved in data-volume folder
Docker run -v data-volume:/var/lib/mysql (image-name) 		[if we run direct this command so docker auto create a volume]





Docker compose 

```bash
version: '3'
services:
  # my-app:
    # image: ${docker-registry}/my-app:1.0
    # ports:
     # - 3000:3000
  mongodb:
    image: mongo
    ports:
     - 27017:27017
    environment:
     - MONGO_INITDB_ROOT_USERNAME=admin
     - MONGO_INITDB_ROOT_PASSWORD=password
    volumes:
     - mongo-data:/data/db
  mongo-express:
    image: mongo-express
    restart: always
    ports:
     - 8080:8081
    environment:
     - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
     - ME_CONFIG_MONGODB_ADMINPASSWORD=password
     - ME_CONFIG_MONGODB_SERVER=mongodb
    depends_on:
     - "mongodb"
volumes:
  mongo-data:
    driver: local
```

If we need a multiple container for a specific application so we can made yaml file to start all containers together

