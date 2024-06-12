
# DevOps Project: CI/CD Pipeline with Jenkins, Docker, and Maven
This project demonstrates a CI/CD pipeline using Jenkins to build, test, and publish a Java application with Maven. Docker is used for containerization, enabling consistent deployment. The built Docker image is then published to DockerHub, ensuring efficient and scalable application delivery.

## Table of Contents
- [Project Overview](#project-overview)
- [Installation](#installation)
- [Usage](#usage)
- [Jenkins Integration](#jenkins-integration)
- [Dockerization](#dockerization)
- [Contact](#contact)
- [Acknowledgements](#acknowledgements)

## Project Overview
Its a sample java application for purpose of Jenkins integration and dockerization. 

## Installation
Instructions on how to install and set up the project locally.
Clone this repository 
``` 
$ git clone https://github.com/anupam1897/cit-project.git  
$ cd cit-project
```

### Prerequisites

1. Jenkins: Follow steps on jenkins website to Install Jenkins. If required install Java too. 
2. The Jenkinsfile will only Execute without error for Windows only.
3. Must have docker installed and user must login using their own docker credentials for pushing image to their dockerhub repository.
``` $ docker login ```
4. Keep docker-daemon running along with jenkins.


## Jenkins Integration
Details on how to integrate the project with Jenkins.

### Jenkinsfile
Jenkinsfile contains the pipeline for the project which build, deploys and pushes image to dockerhub.

### Setup Instructions
In Jenkins, create and new job and follow the steps
1. Configure the job
2. In Pipeline, choose pipeline script from SCM
3. The choose git for SCM
4. Add repository URL: https://github.com/anupam1897/cit-project.git
5. Since it is public repository credentials is not required, leave it to none.
6. In Branch if is not main, change it to main
7. In Script path it should be "Jenkinsfile" (Case-sensitive).

## Dockerization
1. To build image
``` $ docker build -t java-app:v1 .```
2. To create a container using this image
``` $ docker run -d --name "java-app" -p 5000:5000 java-app:v1```
3. After container is up and running, open any browser and search url
``` localhost:5000 ```

### Dockerfile
Dockerfile helps build docker image. Dockerfile in this repo works in two stages - packaging java application and creating image.


### Docker Image
You can find docker image built using this Jenkinsfile and dockerfile at https://hub.docker.com/repository/docker/anupam1897/java-app-v1.0.0

You can also use this image to directly run this app in docker 
``` 
# Pull the Docker image
$ docker pull anupam1897/java-app-v1.0.0:66

# Run the Docker container
$ docker run -p 5000:5000 anupam1897/java-app-v1.0.0:66

```

### Contact
For any query or suggestion email me at anupam1897@gmail.com

### License
You are free to use this repository in any way you want.
