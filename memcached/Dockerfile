FROM memcached:1.5-alpine
LABEL maintainer "Manaki <manakinaoe@gmail.com>"

USER root

RUN apk update --no-cache && \
    apk upgrade --no-cache && \
    apk add --no-cache \
        tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

USER memcache