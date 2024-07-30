<div id="header" align="center">
  <img src="https://media.giphy.com/media/M9gbBd9nbDrOTu1Mqx/giphy.gif" width="100"/>
</div>

<div style="text-align: center;">
  <h1>
    Hey there
    <img src="https://media.giphy.com/media/hvRJCLFzcasrR4ia7z/giphy.gif" width="50px"/>
  </h1>
</div>

<div align="center">
  <img src="https://media.giphy.com/media/dWesBcTLavkZuG35MI/giphy.gif" width="600" height="300"/>
</div>

---

### :woman_technologist: About Me :
I am a Infra/Network Engineer <img src="https://media.giphy.com/media/WUlplcMpOCEmTGBtBW/giphy.gif" width="30"> from Pakistan.

- :telescope: I’m currently working as a Infra/Network engineer and transitioning towards a career in automation.

- :seedling: Exploring new tools for automation and technologies to enhance operational efficiency.

- :zap: In my free time, I actively engage with and practice using various DevOps tools and read tech articles.

- :mailbox: How to reach me: [![Linkedin Badge](https://img.shields.io/badge/-Linkedin-blue?style=flat&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/sarib-wasee-80303113b/)

---

### :hammer_and_wrench: Languages and Tools :

<div>
  <img src="https://github.com/devicons/devicon/blob/master/icons/bash/bash-original.svg" title="Bash" alt="Bash" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/jenkins/jenkins-original.svg" title="Jenkins" alt="Jenkins" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/ansible/ansible-original.svg" title="Ansible" alt="Ansible" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/linux/linux-original.svg" title="Linux"  alt="Linux" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/ubuntu/ubuntu-original.svg" title="Ubuntu" alt="Ubuntu" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/docker/docker-original.svg" title="Docker" alt="Docker" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/yaml/yaml-original.svg" title="Yaml" alt="Yaml " width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/groovy/groovy-original.svg" title="groovy" alt="groovy" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/amazonwebservices/amazonwebservices-plain-wordmark.svg" title="AWS" alt="AWS" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/apache/apache-original-wordmark.svg"  title="Apache" alt="Apache" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/html5/html5-original.svg" title="HTML5" alt="HTML" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/bitbucket/bitbucket-original-wordmark.svg" title="bitbucket" alt="bitbucket" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/gitlab/gitlab-original.svg" title="gitlab" alt="gitlab" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/git/git-original-wordmark.svg" title="Git" **alt="Git" width="40" height="40"/>
</div>



<br/>


# Docker

A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries, and settings. LXC is an old version of the container concept; the new and extended version is Docker, which creates a virtual environment.

## Docker Engine Versions

1. **Version 1**: Creates a single bridge network where all containers can reach each other.
2. **Version 2**: Creates a separate bridge network where all containers in the YAML file can reach each other, but not all containers. Linking containers is not necessary.
3. **Version 3**: Includes all capabilities of Version 2 and much more.

## Docker Engine Components

1. **Docker Daemon**: 
   - The daemon (`dockerd`) is a process that keeps running in the background and waits for commands from the client. It manages various Docker objects.

2. **Docker Client**: 
   - The client (`docker`) is a command-line interface program responsible for transporting commands issued by users.

3. **REST API**: 
   - The REST API acts as a bridge between the daemon and the client. Any command issued using the client passes through the API to reach the daemon.

Docker engine has an embedded DNS, allowing resolution by container name. You can change container IP settings via their Dockerfile. If an image is built, changes cannot be made to the image file; instead, a new Dockerfile must be set up to make changes.

## Simple FAQs

1. **Image**: 
   - Build an application or OS (package, template).

2. **Container**: 
   - Any app or OS running in a container.

3. **Multiple Containers**: 
   - You can use multiple containers with a single image.

4. **Cross-Platform Compatibility**: 
   - Linux containers can run on Windows, but Windows containers can’t run on Linux.



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
