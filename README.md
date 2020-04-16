# docker-only-fleetman
The full set of microservices for Fleetman without needing a Euerka Registry.

Created as a working example for the Docker training course at https://www.virtualpairprogrammers.com/training-courses/Docker-Module-2-for-Java-Developers-training.html?agent=github

Chapter 9 of the course shows how Docker's Overlay Network can exploit Round Robin DNS to support a Microservice Registry - hence making external registries such as Netflix/Spring Cloud Eureka potentially redundant. 

A full extract from the course can be seen here: https://www.virtualpairprogrammers.com/tutorials/0eb05093-8b5a-4d4a-9949-5023ceb64f7f?agent=github

For this version I haven't bothered creating separate repos - each subfolder is a separate Java microservice.


https://github.com/dockersamples/docker-swarm-visualizer

To run:

$ docker run -it -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock dockersamples/visualizer

If port 8080 is already in use on your host, you can specify e.g. -p [YOURPORT]:8080 instead. Example:

$ docker run -it -d -p 5000:8080 -v /var/run/docker.sock:/var/run/docker.sock dockersamples/visualizer

To run with a different context root (useful when running behind an external load balancer):

$ docker run -it -d -e CTX_ROOT=/visualizer -v /var/run/docker.sock:/var/run/docker.sock dockersamples/visualizer

To run in a docker swarm:

$ docker service create \
  --name=viz \
  --publish=8080:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer

