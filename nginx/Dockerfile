
FROM alpine:3.7
LABEL maintainer "Manaki <manakinaoe@gmail.com>"

RUN apk update --no-cache && \
    apk upgrade --no-cache && \
    apk add --no-cache \
        nginx \
        tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata && \
    adduser -S www-data && \
    echo "www-data ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    echo 'www-data:www-data' | chpasswd && \
    rm -rf /var/cache/apk/*

# nginxのconfigファイルを設置
COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY conf/web.conf /etc/nginx/conf.d/web.conf

EXPOSE 80

WORKDIR /var/www

ENTRYPOINT /usr/sbin/nginx -g "daemon off;" -c /etc/nginx/nginx.conf