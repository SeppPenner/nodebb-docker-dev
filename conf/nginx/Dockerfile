FROM alpine
MAINTAINER qgp9 

# Install nginx 
RUN apk update && apk upgrade && apk update
RUN apk add --update nginx bash && \
    rm -rf /var/cache/apk/*  

# Expose the ports for redis
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
