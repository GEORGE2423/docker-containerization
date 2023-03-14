Pull  the grafana image

docker pull grafana/grafana:latest

Grafana Docker image
Run the Grafana Docker container
Start the Docker container by binding Grafana to external port 3000.
docker run -d --name=grafana -p 3000:3000 grafana/grafana
docker run -d --name=grafana -p 3000:3000 grafana/grafana