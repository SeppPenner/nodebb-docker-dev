FROM alpine
MAINTAINER qgp9 

# Install Node.js
RUN apk update && apk upgrade && apk update
RUN apk add --update  git curl bash
RUN apk add --update nodejs

# NodeBB
RUN apk add --update imagemagick git curl bash && rm -rf /var/cache/apk/*

ENV NODEBB_DIR /opt/nodebb/
WORKDIR ${NODEBB_DIR}

VOLUME  ${NODEBB_DIR}

EXPOSE  4567

ENV NODE_ENV=production \
    daemon=false \
    silent=false

# Define default command.
CMD ["npm","start"]
