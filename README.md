#Nginx and lua modules to achieve fast rewrite scenario

## Docker-Compose Running Command

```bash
docker-compose up -d
docker-compose down
```

```bash
#background mode
docker-compose down && docker-compose build %% docker-compose up -d 
#foreground mode
docker-compose down && docker-compose build %% docker-compose up 
```

```bash
#url for testing redis + lua rewrite
curl http://localhost:10080/relua/anything?eid=test&name=irene&pid=1


~/go/bin/boom -n 900 -c 900 -disable-keepalive http://localhost:10080/relua/anything?eid=test&name=irene&pid=1
```

```bash commands for etcd cluster
docker exec edgeservice_nginx_1 ps axu

curl -L http://127.0.0.1:2379/health

curl http://127.0.0.1:2379/v2/keys/message -XPUT -d value="Hello world" 
curl http://127.0.0.1:2379/v2/keys/message
curl http://127.0.0.1:2379/v2/keys/message -XPUT -d value="Hello etcd"
curl http://127.0.0.1:2379/v2/keys/message -XDELETE

curl http://127.0.0.1:2379/v2/keys/foo -XPUT -d value=bar -d ttl=5
curl http://127.0.0.1:2379/v2/keys/foo
curl http://127.0.0.1:2379/v2/keys/foo -XPUT -d value=bar -d ttl= -d prevExist=true
curl http://127.0.0.1:2379/v2/keys/foo?wait=true


curl http://127.0.0.1:2379/v2/keys/queue -XPOST -d value=Job1

```


#docker swarm 
```bash

docker service create \
  --replicas 10 \
  --name redis \
  --update-delay 10s \
  --update-parallelism 2 \
  edgeservice_nginx:latest

services:
  nginx:
    build: './nginx-lua-edge-service'
    ports:
     - "10080:80"
     - "10443:443"
    volumes:
     - ./nginx-lua-edge-service/data:/data
    links:
      - redis
  
```