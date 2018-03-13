#NGNIX and luda as edge service 

## Docker Running Command

```bash
export NGINX_LUA_HOME="/root/tony/edge_service/nginx-lua-edge-service"
docker build -t nginx_lua_edge .
docker build -t bigdata/nginx_lua_edge .
docker rm -f nginx_lua_edge
docker run --name nginx_lua_edge -d \
    -v $NGINX_LUA_HOME/data/etc/nginx:/data/etc/nginx \
    -p 10080:80 \
    nginx_lua_edge 
docker exec -it nginx_lua_edge /bin/bash
docker logs nginx_lua_edge

#check whether amplify is running 
docker exec -it nginx_lua_edge /bin/bash
docker exec nginx_lua_edge ps axu

#check amplify log
docker exec nginx_lua_edge tail /var/log/amplify-agent/agent.log
docker exec nginx_lua_edge tail /var/log/nginx/access.log 
docker exec nginx_lua_edge tail /var/log/nginx/error.log 


# update nginx.conf and reload nginx
cp -f /data/etc/nginx/nginx.conf /etc/nginx/nginx.conf && \
nginx -s reload

```


docker rm -f nginx_lua_edge
docker run --name nginx_lua_edge -d \
    -P nginx_lua_edge


docker run -d -p 5000:5000 --restart=always --name registry \
-v `pwd`/certs:/certs \
-v `pwd`:/var/lib/registry \
-e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt \
-e REGISTRY_HTTP_TLS_KEY=/certs/domain.key \
registry:2.5     