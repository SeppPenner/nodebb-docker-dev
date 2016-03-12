FROM alpine
MAINTAINER qgp9 

# Install redis
RUN apk update && apk upgrade && apk update
RUN apk add --update redis bash && \
    rm -rf /var/cache/apk/*  
#RUN echo -e 'vm.overcommit_memory = 1' >> /etc/sysctl.conf

RUN mkdir /data
WORKDIR /data

# Expose the ports for redis
EXPOSE 6379
CMD ["redis-server", "/etc/redis.conf"]
