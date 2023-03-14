Our system requirements should be taken into account when provisioning the Docker container.

Default user is admin and the uniquely generated password can be found in the admin.password file inside the volume. See Persistent Data for information about the volume.

It can take some time (2-3 minutes) for the service to launch in a new container. You can tail the log to determine once Nexus is ready:

$ docker logs -f nexus
Installation of Nexus is to /opt/sonatype/nexus.

A persistent directory, /nexus-data, is used for configuration, logs, and storage. This directory needs to be writable by the Nexus process, which runs as UID 200.

There is an environment variable that is being used to pass JVM arguments to the startup script

INSTALL4J_ADD_VM_PARAMS, passed to the Install4J startup script. Defaults to -Xms2703m -Xmx2703m -XX:MaxDirectMemorySize=2703m -Djava.util.prefs.userRoot=${NEXUS_DATA}/javaprefs.
This can be adjusted at runtime:

$ docker run -d -p 8081:8081 --name nexus -e INSTALL4J_ADD_VM_PARAMS="-Xms2703m -Xmx2703m -XX:MaxDirectMemorySize=2703m -Djava.util.prefs.userRoot=/some-other-dir" sonatype/nexus3
Of particular note, -Djava.util.prefs.userRoot=/some-other-dir can be set to a persistent path, which will maintain the installed Nexus Repository License if the container is restarted.

Be sure to check the memory requirements when deciding how much heap and direct memory to allocate.

Another environment variable can be used to control the Nexus Context Path

NEXUS_CONTEXT, defaults to /
This can be supplied at runtime:

$ docker run -d -p 8081:8081 --name nexus -e NEXUS_CONTEXT=nexus sonatype/nexus3
Persistent Data
There are two general approaches to handling persistent storage requirements with Docker. See Managing Data in Containers for additional information.
 ##############################  Nexus configurations
Use a docker volume. Since docker volumes are persistent, a volume can be created specifically for this purpose. This is the recommended approach.
$ docker volume create --name nexus-data
$ docker run -d -p 8081:8081 --name nexus -v nexus-data:/nexus-data sonatype/nexus3
Mount a host directory as the volume. This is not portable, as it relies on the directory existing with correct permissions on the host. However it can be useful in certain situations where this volume needs to be assigned to certain specific underlying storage.
$ mkdir /some/dir/nexus-data && chown -R 200 /some/dir/nexus-data
$ docker run -d -p 8081:8081 --name nexus -v /some/dir/nexus-data:/nexus-data sonatype/nexus3
