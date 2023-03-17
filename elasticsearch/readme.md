Running in Development Mode:
Create user defined network (useful for connecting to other services attached to the same network (e.g. Kibana)):
create a docker network: 

docker network create somenetwork

Run Elasticsearch:

$ docker run -d --name elasticsearch --net somenetwork -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:tag

url :  https://hub.docker.com/_/elasticsearch