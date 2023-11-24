# Docker Crash Course

Tasks and notes from crash course.

[Source](https://www.youtube.com/watch?v=pg19Z8LL06w)



## Video progress

- [x] [Section 01](#) - Intro and Course Overview
- [x] [Section 02](#) - What is Docker?
- [x] [Section 03](#) - What problems Docker solves in development and deployment process
- [ ] [Section 04](#) - Virtual Machine vs Docker
- [ ] [Section 05](#) - Install Docker
- [ ] [Section 06](#)- Docker Images vs Containers
- [ ] [Section 07](#) - Docker Registries
- [ ] [Section 08](#) - Main Docker Commands - Pull and Run Docker containers
- [ ] [Section 09](#) - Port Binding
- [ ] [Section 10](#) - Start and Stop containers
- [ ] [Section 11](#) - Private Docker Registries
- [ ] [Section 12](#) - Registry vs Repository
- [ ] [Section 13](#) - Dockerfile - Dockerize Node.js app
- [ ] [Section 14](#) - Build Image
- [ ] [Section 15](#) - Docker UI Client
- [ ] [Section 16](#) - Overview: Docker in complete software development lifecycle
- [ ] [Section 17](#) - Where to go from here

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
    - Vm images, a couple of **GB**
    - Vm takes **minutes** to start
    - Vm is running with all **OS**

15:00