# Docker Crash Course

Tasks and notes from crash course.

[Source](https://www.youtube.com/watch?v=pg19Z8LL06w)



## Video progress

- [x] Section 01 - Intro and Course Overview
- [x] [Section 02](#What-is-docker) - What is Docker?
- [x] Section 03 - What problems Docker solves in development and deployment process
- [x] [Section 04](#Virtual-Machine-vs-Docker) - Virtual Machine vs Docker
- [x] Section 05 - Install Docker
- [x] [Section 06](#Docker-Images-vs-Containers) - Docker Images vs Containers
- [x] [Section 07](#Docker-Registries) - Docker Registries
- [x] [Section 08](#Docker-Image-Versions) - Docker Image Versions
- [x] [Section 09](#Pull-and-Run-Docker-containers) - Main Docker Commands - Pull and Run Docker containers
- [x] [Section 10](#Port-Binding) - Port Binding
- [x] [Section 11](#Start-and-Stop-containers) - Start and Stop containers
- [x] [Section 12](#Private-Docker-Registries) - Private Docker Registries
- [x] [Section 13](#Registry-vs-Repository) - Registry vs Repository
- [x] [Section 14](#Dockerfile) - Dockerfile - Dockerize Node.js app
- [x] [Section 15](#Build-Image) - Build Image
- [x] [Section 16](#Docker-UI-Client) - Docker UI Client
- [x] [Section 17](#Docker-in-complete-software-development-lifecycle) - Overview: Docker in complete software development lifecycle
- [x] Section 18 - Where to go from here

#### What is docker

 - Before containers, all developers needed to install their own setups of tools for their specific needs.
    - Os specific
    - Configuration specific
    - Etc

#### Development/Deployment with Docker 

<img src="dockerDevelopementProcess.JPG" alt="alt text" width="500"/>

1. All these decencies are inside container. 
2. As **developer,** you just need to execute **one docker command** and get **docker container package** `docker run postgres`

- Docker standardizes process of running any service on any local dev environment
    - More time for development than setting up configuration
    - With docker you can have same service running on local device whiteout any conflict 

<img src="deploymentProcessWithConainers.JPG" alt="alt text" width="500"/>

- With containers → DevOps team just needs to fetch and run **Docker artifact**

#### Virtual Machine vs Docker

-  Docker virtualize **OS Application Layer**
- Virtual machine virtualizes
**OS Application Layer** and **OS kernel** → Meaning virtualizes **complete operating system**

- What it means:
    - Docker image is, a couple of **MB**
    - Dockers container takes **seconds** to start
    - Dockers compatible only with **Linux distros**
    - Vm images, a couple of **GB**
    - Vm takes **minutes** to start
    - Vm is running with all **OS**

<img src="runningDockerProblem.JPG" alt="alt text" width="600"/>

1. Docker can't run Linux based docker image in **Windows Host**  

- Docker Desktop
    - Linux containers run on Windows or macOS
    - This is solved with **Hypervisor layer** with small Linux distro.
    `install Docker Desktop`

### Docker Images vs Containers

- **Docker images** are like **.jar** a file packaged in containers.
    - It has compiled code
    - It also has **complete environment configuration**
        - Application, any services(Js app)(node, npm) needed, Os Layer(Linux)
    - Add env variables,
    create directories

- **Docker Container** is running image
- You can one you can run multiple container

<img src="imagesAndContiners.JPG" alt="alt text" width="200"/>

1. Images can be run in containers

- `docker images` Show what images we have locally

- `docker ps` List running containers

### Docker Registries

- There are images stored in Docker Register

- Official images are available from applications like Redis, Mongo, Postgres etc.
    - There can be verified "Official" images or unofficial ones.

- One the biggest docker register store is DockerHub
    - One of Reddis [Images](https://hub.docker.com/_/redis) 

<img src="dockerOfficialImages.JPG" alt="alt text" width="500"/>

 ### Docker Image Versions

<img src="imageVersioning.JPG" alt="alt text" width="500"/>

- If you need specific version, you can choose specific docker image which has right **tag**
    - `latest` is the latest which was build

### Pull and Run Docker containers

- To download image `docker pull nginx:1.23`

<img src="dockerPull.JPG" alt="alt text" width="500"/>

- To list images `docker images`

- Running images into container `docker run nginx:1.23`
    - With `-d` stop blocking

- Docker generates random name automatically

<img src="dockerRun.JPG" alt="alt text" width="400"/>

### Port Binding

<img src="portBinding.JPG" alt="alt text" width="400"/>

- We need to **expose** container **ports**
    - This is done with **Port Binding** 

<img src="runningInport.JPG" alt="alt text" width="500"/>

- You can see what ports containers are running in

<img src="exposingImageToLocalHostPorts.JPG" alt="alt text" width="300"/>

1. Port inside container
2. Exposing port to local host

- We can expose ports to localhost when creating container with special **flag**

<img src="dockerStop.JPG" alt="alt text" width="300"/>

<br>

<img src="dockerpublish.JPG" alt="alt text" width="300"/>

- We can publish ports when creating image with **flag** 

`docker run -d -p 9000:80 nginx:1.23`

<img src="dockerpublish.JPG" alt="alt text" width="300"/>

- With following port structure

<img src="portStructure.JPG" alt="alt text" width="300"/>

<br>

<img src="afterRunningContainerWithHostInformation.JPG" alt="alt text" width="500"/>

1. After running with opening with following ports
    - We can see what is being mapped on 

<br>

- Now we can see its deployed into port 9000

<img src="deployedInto9000.JPG" alt="alt text" width="500"/>

- To expose logs from docker 
    - `docker logs 6cb988ce6e05`, where last one is docker id

- It's standard to bind same port into container and which is exposed outside of container

### Start and Stop containers

- Docker run always creates new container

- To see all container which docker have created. You can use 

`docker ps -a`
- To start container you can use `docker start {container} = start one or more stopped containers`. Example `docker logs 6cb988ce6e05`

### Private Docker Registries

- When companies, creates their own public private docker registries.

### Registry vs Repository

<br>

<img src="registeryVsRepository.JPG" alt="alt text" width="400"/>

### Dockerfile

- We want to build our docker image, when our application version is finished
    - We do this by writing "definition" how to build image
        - This is called **docker file**

<img src="dockerBaseImage.JPG" alt="alt text" width="400"/>

- Telling to build base image **FROM** base image

<br>

<img src="from.JPG" alt="alt text" width="300"/>

- In docker file you can run Linux commands!
    - This is done with **RUN** directive

- **COPY** copies files from src and adds them to containers path

- **WORKDIR /app** changes working directly inside docker

- Last command in docker file is **CMD**

<img src="cmd.JPG" alt="alt text" width="400"/>

#### Example of docker file

```

FROM node:19-alpine

COPY package.json /app/
COPY src /app/

# COPY src /app/, last / is important. Docker will create new folder if there is no 

WORKDIR /app

RUN npm install

CMD ["node", "server.js"]

```

### Build Image

<img src="dockerBuild.JPG" alt="alt text" width="300"/>

<br>

<img src="tag.JPG" alt="alt text" width="300"/>


- Building image `docker build -t node-app:1.0 .`
    - Last one is location of Dockerfile

<img src="creatingImage.JPG" alt="alt text" width="500"/>

- You can see image is created in layers

- We can run our newly created image `docker run -d -p 3000:3000 node-app:1.0`

- We can see that our application inside docker is running and its being exposed to `localhost:3000`

<img src="runningIn3000Verify.JPG" alt="alt text" width="500"/>

### Docker UI Client

- Same tool is found in UI

<img src="dockerUI.JPG" alt="alt text" width="500"/>

### Docker in complete software development lifecycle

- CI server can create docker image automatically 

<img src="dockerBuildSycle.JPG" alt="alt text" width="500"/>

1. After commit, **CI server** can be configured with to push and create docker image into **Private Repository**

### Additional about docker

- We can connect docker app and MySQL with help of **network**

<img src="dockerNetworks.JPG" alt="alt text" width="500"/>

1. When running docker container they are running in isolated networks

- Listing all network `docker network ls`

- Creating docker network `docker network create spring-net`

- Connecting our **container** with given **network** `docker network connect spring-net mysqldb`

- Inspecting our container for attached networks `docker container inspect mysqldb`

- We can attach container to **certain network** when starting the container

```
docker run -p 9090:8080 --name app --net spring-net -e MYSQL_HOST=mysqldb -e MYSQL_USER=root -e MYSQL_PASSWORD=root -e MYSQL_PORT=3306 app
```

## Creating MySQL running in localhost container

- Starting and pulling and starting MySQL image `docker run -d -p 3307:3306 --name mysqldb -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=user_rest_demo mysql`

- To test connection `localhost:3007` and configure `allowPublicKeyRetrieval` to **true**

## Docker Volume

<img src="dockerVolume.JPG" alt="alt text" width="500"/>

- When restarting application data is lost, we can use **volumes** to keep data saved