FROM redis



ARG BIND_IP
ARG BIND_PORT
ARG PASS
ARG MASTER_IP
ARG MASTER_PORT
ARG ROLE
ARG IP_ADDR

RUN \
    mkdir -p /log && \
    chmod 777 /log 

COPY ./redis-server.conf /usr/local/etc/redis/redis.conf
RUN chmod 777 /usr/local/etc/redis/redis.conf
RUN echo ""  >> /usr/local/etc/redis/redis.conf
RUN echo  "bind $BIND_IP" >> /usr/local/etc/redis/redis.conf
RUN echo ""  >> /usr/local/etc/redis/redis.conf
RUN echo "port $BIND_PORT" >> /usr/local/etc/redis/redis.conf
RUN echo  "requirepass '$PASS'" >> /usr/local/etc/redis/redis.conf
RUN echo ""  >> /usr/local/etc/redis/redis.conf
RUN echo  "masterauth '$PASS'" >> /usr/local/etc/redis/redis.conf
RUN echo ""  >> /usr/local/etc/redis/redis.conf
RUN echo  "logfile '/log/redis-$IP_ADDR.log'" >> /usr/local/etc/redis/redis.conf
RUN echo ""  >> /usr/local/etc/redis/redis.conf
#RUN echo  "dir '/data/$IP_ADDR'" >> /usr/local/etc/redis/redis.conf
RUN echo ""  >> /usr/local/etc/redis/redis.conf
RUN if [ "$ROLE" != "master" ]; then echo  "slaveof $MASTER_IP $MASTER_PORT" >> /usr/local/etc/redis/redis.conf; fi


# Expose ports.
EXPOSE $bind_port
CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]