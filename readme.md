# Installation
## Build the Jenkins BlueOcean Docker Image if arm64 version 
```
docker build -f <name-of-dockerfile> --platform=linux/arm64  .
```
## Build the Jenkins BlueOcean Docker Image if amd64 version 

```
docker build -f <name-of-dockerfile> --platform=linux/amd64 .
```
## Run the Container use docker-compose
```
docker-compose -f <name-of-file-compose> up -d  
```

## Get the Password
```
docker exec <name of containaer or container-id> cat /var/jenkins_home/secrets/initialAdminPassword
```
## Connect to the Jenkins
```
https://localhost:8080/
```

## Installation Reference:
https://www.jenkins.io/doc/book/installing/docker/


## alpine/socat container to forward traffic from Jenkins to Docker Desktop on Host Machine

https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin
```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
docker inspect <container_id> | grep IPAddress
```

## Using my Jenkins agent
```
docker pull redheaven/agent:v1
```
