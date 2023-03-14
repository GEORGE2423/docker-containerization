How to use this image.
Note: as of docker-library/tomcat#181, the upstream-provided (example) webapps are not enabled by default, per upstream's security recommendations, but are still available under the webapps.dist folder within the image to make them easier to re-enable.

Run the default Tomcat server (CMD ["catalina.sh", "run"]):

$ docker run -it --rm tomcat:9.0
You can test it by visiting http://container-ip:8080 in a browser or, if you need access outside the host, on port 8888:

$ docker run -it --rm -p 8888:8080 tomcat:9.0
You can then go to http://localhost:8888 or http://host-ip:8888 in a browser (noting that it will return a 404 since there are no webapps loaded by default).

The default Tomcat environment in the image is:

CATALINA_BASE:   /usr/local/tomcat
CATALINA_HOME:   /usr/local/tomcat
CATALINA_TMPDIR: /usr/local/tomcat/temp
JRE_HOME:        /usr
CLASSPATH:       /usr/local/tomcat/bin/bootstrap.jar:/usr/local/tomcat/bin/tomcat-juli.jar
The configuration files are available in /usr/local/tomcat/conf/. By default, no user is included in the "manager-gui" role required to operate the "/manager/html" web application. If you wish to use this app, you must define such a user in tomcat-users.xml.