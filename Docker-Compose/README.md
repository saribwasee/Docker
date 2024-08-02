### Docker Compose Concepts

Docker Compose allows you to define and manage multi-container applications in a single YAML file. This simplifies the complex task of orchestrating and coordinating various services, making it easier to manage and replicate your application environment. If we need a multiple container for a specific application so we can made yaml file to start all containers together

#### Key Concepts:

1. **Services**: A service in Docker Compose is a running container defined in the `docker-compose.yaml` file. Each service runs one image and defines the set of options (e.g port bindings, volume mappings, and environment variables) that determine how the container should be run.

2. **Containers**: These are the instances of the services defined in your `docker-compose.yaml` file. Docker Compose creates and manages these containers.

3. **Networks**: Docker Compose sets up a default network for your application. Services in the same network can communicate with each other by using their service names.

4. **Volumes**: Volumes allow you to persist data between container restarts or container die. They can be used to share data between services or to ensure data is not lost when a container is recreated.

5. **Configuration File**: The `docker-compose.yaml` file is where you define your application services, networks, and volumes.

#### Example `docker-compose.yaml`:

Here's an example `docker-compose.yml` file for a simple web application with a web server and a database service:

```yaml
version: '3.8'

services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    depends_on:
      - db

  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: example
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

#### Detailed Steps:

1. **Version**: 
   - Specifies the version of the Docker Compose file format.

2. **Services**:
   - **web**: Defines a service named `web`.
     - **image**: Specifies the Docker image to use (nginx:latest).
     - **ports**: Maps port 80 on the host to port 80 in the container.
     - **volumes**: Mounts the `./html` directory from the host to `/usr/share/nginx/html` in the container.
     - **depends_on**: Specifies dependencies. The `web` service depends on the `db` service, ensuring the `db` service starts first.
   - **db**: Defines a service named `db`.
     - **image**: Specifies the Docker image to use (mysql:latest).
     - **environment**: Sets environment variables (`MYSQL_ROOT_PASSWORD`).
     - **volumes**: Mounts a named volume `db_data` to `/var/lib/mysql` in the container.

3. **Volumes**:
   - **db_data**: Defines a named volume for the database service to persist data.

#### Key Commands:

- **Starting Services**: `docker-compose up`
  - This command builds, (re)creates, starts, and attaches to containers for a service.
- **Stopping Services**: `docker-compose down`
  - This command stops and removes containers, networks, volumes, and images created by `up`.
- **Viewing Logs**: `docker-compose logs`
  - Displays log output from services.
- **Running a One-Off Command**: `docker-compose run`
  - Run a one-off command against a service (e.g., `docker-compose run web bash`).

#### Use Cases:

1. **Development Environments**: Quickly set up isolated development environments with all necessary services.
2. **Testing**: Spin up containers to run tests against a fresh environment.
3. **Multi-Container Applications**: Manage applications with multiple interconnected services, such as web servers, databases, and caching services.
4. **CI/CD Pipelines**: Integrate Docker Compose into CI/CD pipelines to build, test, and deploy applications consistently across different environments.

Docker Compose simplifies the process of managing multi-container applications, making it easier to configure, deploy, and scale applications composed of multiple services.




## Docker Compose Sample

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

