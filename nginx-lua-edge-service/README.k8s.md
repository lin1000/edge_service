#NGNIX and luda as edge service 

## Docker Running Command

```bash
export NGINX_LUA_HOME="/root/tony/edge_service/nginx-lua-edge-service"
docker build -t 10.106.178.130:19999/nginx_lua_edge .
docker rm -f nginx_lua_edge
docker run --name nginx_lua_edge -d \
    -v $NGINX_LUA_HOME/data/:/data/ \
    -p 10080:80 \
    10.106.178.130:19999/nginx_lua_edge 
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

kubectl get pods
```k8s exec <POD_NAME> -it /bin/bash
kubectl logs nginx-edge-service-68d5679949-4jc5s
kubectl exec nginx-edge-service-7cdf7755d6-4jc5s -i -t /bin/bash
apt-get update && apt-get -y install net-tools
/usr/sbin/nginx -c "/etc/nginx/nginx.conf" -t
/usr/sbin/nginx -s reload -c "/etc/nginx/nginx.conf" -g "daemon off;"
```

加入volume並掛載正破後，解決nginx無法啟動的問題