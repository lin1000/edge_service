FROM redis:4.0.7
RUN mkdir -p /usr/local/etc/redis/
COPY ./etc/redis/redis.conf /usr/local/etc/redis/redis.conf

CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]