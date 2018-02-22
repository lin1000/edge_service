#NGNIX as edge service 

## Docker Running Command

```bash
docker build -t redis_edge .
docker rm -f redis_edge
docker run --net=bridge --name redis_edge -d -p 6379:6379  redis_edge 
docker rm -f redis_edge
docker run  --name redis_edge -d -p 6379:6379  redis_edge 

docker exec -it redis_edge service amplify-agent start
docker logs redis_edge
#check whether amplify is running 
docker exec redis_edge ps axu
```

## How to Test Redis
```bash
docker exec -it redis_edge /bin/bash
redis-cli ping  
```

```bash
$ redis-cli                                                      
redis 127.0.0.1:6379> ping
PONG
redis 127.0.0.1:6379> set mykey somevalue
OK
redis 127.0.0.1:6379> get mykey
"somevalue"
```

##Features
docker rm -f test
docker run --net=host --name test -d -p 63799:6379  redis_edge 
r = redis.Redis(host='127.0.0.1',port=6379,db=0)