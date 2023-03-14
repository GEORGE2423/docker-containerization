To run, binding the exposed port 8081 to the host, use:

$ docker run -d -p 8081:8081 --name nexus sonatype/nexus3
When stopping, be sure to allow sufficient time for the databases to fully shut down.

docker stop --time=120 <CONTAINER_NAME>
To test:

$ curl http://localhost:8081/

Accessessing the docker container: 

docker exec  -it    nexus     bash 
