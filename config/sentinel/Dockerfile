FROM redis

ARG BIND_IP
ARG BIND_PORT
ARG PASS
ARG MASTER_IP
ARG MASTER_PORT
ARG QORUM
ARG DOWN_AFTER_MS
ARG FAILOVER_TIME_OUT
ARG IP_ADDR

RUN \
    mkdir -p /log && \
    chmod 777 /log 

COPY redis-sentinel.conf /usr/local/etc/redis/sentinel.conf
RUN chmod 777 /usr/local/etc/redis/sentinel.conf
RUN \
   echo  "bind $BIND_IP" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "port $BIND_PORT" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "sentinel monitor redis-cluster $MASTER_IP $MASTER_PORT $QORUM" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "sentinel auth-pass redis-cluster $PASS" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "sentinel down-after-milliseconds redis-cluster $DOWN_AFTER_MS" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "sentinel failover-timeout redis-cluster $FAILOVER_TIME_OUT" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "" >> /usr/local/etc/redis/sentinel.conf && \
   echo  "logfile '/log/redis-sentinel-$IP_ADDR.log'" >> /usr/local/etc/redis/sentinel.conf 



# Expose ports.
EXPOSE $bind_port
CMD [ "redis-sentinel", "/usr/local/etc/redis/sentinel.conf" ]