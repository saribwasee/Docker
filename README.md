# Docker

A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings. LXC old version of container concept new and extended versions is docker which create a virtual environment.


- Docker engine of different version of yaml file
1.	Version 1: create a single bridge network where all containers can be reachable
2.	Version 2: Create a separate bridge network where all containers in the yaml file can be reachable not all containers
So, we not need to links containers
3.	Version 3:  All capabilities of Version 2 and much more

The engine consists of three major components:
1.	Docker Daemon: The daemon (dockerd) is a process that keeps running in the background and waits for commands from the client. The daemon is capable of managing various Docker objects.
2.	Docker Client: The client  (docker) is a command-line interface program mostly responsible for transporting commands issued by users.
3.	REST API: The REST API acts as a bridge between the daemon and the client. Any command issued using the client passes through the API to finally reach the daemon.

Docker engine have embedded DNS we can resolve by container name, we can change container IP settings by their Dockerfile if image build so we cant changes in image file we again set up new docker file to make any changes.

Simple FAQs Questions
Image (Build an application or OS) [package, template]
Container (Any App or OS which are running in container)
We can use multiple containers with a single image
Linux containers can be run in windows but windows containers can’t run on linux


```bash
Some Commands
Docker pull image								[download image from dockerhub]
Docker rmi image								[remove image from the machine]
Docker run -ti (container-name) 						[I = interactive mode]
Docker container ls 								[show running containers]
Docker run -d –name (name) -p (port host:container = 80:8400) image-name	[Different port mapping on host to container]
Docker container inspect (image-name or container ID)				[To check the container details]
Docker exec -ti (container-name or container ID) bash				[interact running container with cli mode]	
Docker exec -ti (container-name or container ID) cat /tmp/file			[run any command without interact container]
Docker run -v /opt/datadir:var/lib/mysql (image-name)				[Data map into host]
Docker run -e (Code which execute) image-name 					[environment variable can be changed if set up ENV in image file]
docker exec -it (cont-ID) -u 0 /bin/bash					[We can interact with any container image with root]

 ```


Creating my own image

```bash
FROM Ubuntu								[Base ubuntu layer]
RUN apt-get update							[changes in apt packages]
RUN apt-get install python						[installing python packages]
RUN pip install flask							[changes in pip packages]
RUN pip install flask-mysql						[changes in pip packages]
COPY . /opt source-code							[Copy code from our host machine]
ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run			[update the entry point with flask command]
```

Dockerfile must be contains in your application folder and file name is exactly same (Dockerfile)

```bash
Docker build dockerfile -t name/mycustom-app
```




## Docker Default Networks

### Network Types

| Type   | Description                |
|--------|----------------------------|
| Bridge | Default network, containers are connected to an internal bridge. |
| None   | Containers are isolated from the network. |
| Host   | Containers share the host’s network stack. |

### Docker Run Examples

- **Bridge Network** (default)
  ```bash
  docker run ubuntu
  ```

- **None Network**
  ```bash
  docker run ubuntu --network=none
  ```

- **Host Network**
  ```bash
  docker run ubuntu --network=host
  ```

### Network Details

- **Private Internal Network**
  - Default IP Range: `172.17.0.0`

- **None & Host Network**
  - Containers are isolated (None network) or share the host’s network stack (Host network).

- **Port Mapping**
  - Access to Container: Map a port with the host machine.
  - Isolated Networks: Containers are isolated in their own networks.
  - Host Network: Same port will be used for the container as the host.




## Docker Volume

### Volume Types

- **Bind Mounts**
  - Syntax: `Host_dir:Cont_dir`

- **Anonymous Volumes**
  - Syntax: `:Cont_dir`

- **Named Volumes**
  - Syntax: `name:Cont_dir`

### Using Docker Volumes

- **Creating a Named Volume**
  ```bash
  docker volume create data-volume
  ```
  - Default Volume Path: `/var/lib/docker/volume/data-volume`

- **Mapping Volume into Container**
  ```bash
  docker run -v data-volume:/var/lib/mysql (image-name)
  ```
  
- **Automatic Volume Creation**
   - If the volume `data-volume` does not exist, Docker will automatically create it.

  ```bash
  docker run -v data-volume:/var/lib/mysql (image-name)
  ```

**Persistent Data Storage**
  - When the container is destroyed, all data is saved in the `data-volume` folder.




## Docker compose

- Docker Compose allows you to define and manage multi-container applications in a single YAML file. This simplifies the complex task of orchestrating and coordinating various services, making it easier to manage and replicate your application environment. If we need a multiple container for a specific application so we can made yaml file to start all containers together

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
