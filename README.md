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
```