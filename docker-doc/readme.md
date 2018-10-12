### Docker Resource

[A Curated List Of Docker Resources](https://github.com/veggiemonk/awesome-docker)

***Starts the Containers***

Builds, (re)creates, starts, and attaches to containers for a service.
Unless they are already running, this command also starts any linked services. [Docker up](https://docs.docker.com/compose/reference/up)
```cli
docker-compose up
```
***Stops the Containers***

Stops containers and removes containers, networks, volumes, and images created by up. [Docker down](https://docs.docker.com/compose/reference/down)
```cli
docker-compose down
```
***Shows what Containers are running.***

Lists containers. [Docker ps](https://docs.docker.com/compose/reference/ps)
```cli
docker ps -a
```
***Set port***

Runs a one-time command against a service. [Docker run](https://docs.docker.com/compose/reference/run)
```cli
docker run -p 8080:80
```
***Remove Containers***

Removes stopped service containers. [Docker rm](https://docs.docker.com/compose/reference/rm)


```cli
docker rm container id
```
***
***Run Container***
```cli
docker run -d name web1 -p 8081:80 tutum/hello-world
```
Results
- ***container name:*** web1
- ***port:*** localhost: 8081
- ***wep app:*** tutum/hello-world
