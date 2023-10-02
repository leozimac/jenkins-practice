# jenkins-practice
A simple Jenkins project to practice how to create and manage pipelines.

## To build the docker image
```docker build -t myjenkins-blueocean:2.414.2-1 .```

## Create a bridge network
```docker network create jenkins```

## Run the image as a container using the command:
```
docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.414.2-1
```

## Get the initial admin password from the docker container
```
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

## Acces the shell of the container
```
docker exec -it jenkins-blueocean bash
```