FROM mysql:8
LABEL maintainer "Manaki <manakinaoe@gmail.com>"

COPY ./conf/charaset.cnf /etc/mysql/conf.d/
COPY ./conf/native.cnf /etc/mysql/conf.d/
COPY ./conf/sql_mode.cnf /etc/mysql/conf.d/
COPY ./conf/tuning.cnf /etc/mysql/conf.d/

RUN mkdir /var/log/mysql \
    touch /var/log/mysql/query.log && \
    touch /var/log/slow.log && \
    chmod -R 777 /var/log/mysql && \
    chmod -R 644 /etc/mysql/conf.d/charaset.cnf && \
    chmod -R 644 /etc/mysql/conf.d/native.cnf && \
    chmod -R 644 /etc/mysql/conf.d/sql_mode.cnf