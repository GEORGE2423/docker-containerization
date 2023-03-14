You need at least one other mariadb/mysql-container to link it to Friendica.

The apache image contains a webserver and exposes port 80. To start the container type:

$ docker run -d -p 8080:80 --network some-network friendica

Now you can access the Friendica installation wizard at http://localhost:8080/ from your host system.