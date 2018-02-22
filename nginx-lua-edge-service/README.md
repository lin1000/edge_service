#NGNIX and luda as edge service 

## Docker Running Command

```bash
export NGINX_LUA_HOME="/Users/lin1000/github/nginx-lua-edge-service"
docker build -t nginx_lua_edge .
docker rm -f nginx_lua_edge
docker run --name nginx_lua_edge -d \
    -v $NGINX_LUA_HOME/etc/nginx:/data/etc/nginx \
    -p 10080:80 \
    -p 10081:81 \
    --link=redis_edge \
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

/usr/sbin/nginx -c "/data/etc/nginx/nginx.conf" -t && \
    /usr/sbin/nginx -s reload -c "/data/etc/nginx/nginx.conf" -g "daemon off;"

# check how may clients and connections 
redis-cli CLIENT LIST | sed -n 's|.*addr=\(.*\)\:.*|\1|p' | sort | uniq -c
```
