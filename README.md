# docker_lemp

lemp環境

## セットアップ手順

### 共通項目

#### nginx/conf/web.conf.defaultを編集

**作業ディレクトリ:docker_lemp**

```bash
$ cp nginx/conf/web.conf.default nginx/conf/web.conf
$ vi nginx/conf/web.conf

~~~省略
server_name  <環境に合わせてここにアドレスを記入>;

# 例 (半角スペース区切りで複数可能)
# server_name localhost 192.168.99.100 penguin.linux.test
```

#### docker-compose.ymlを編集

**作業ディレクトリ:docker_lemp**

```bash
$ cp docker-compose.yml.default docker-compose.yml
$ vi docker-compose.yml

~~~省略
# 以下の記載が2箇所あります。
# ※2箇所とも同じボリュームパス
volumes:
  - <プロジェクトのボリュームパス>:/var/www:cached

# 例
volumes:
  - /c/workspace:/var/www:cached
```

### 一括ビルドしたい人の手順

**作業ディレクトリ:docker_lemp**

```bash
$ docker-compose build
```

### サービス毎にビルドしたい人の手順

**作業ディレクトリ:docker_lemp**

#### nginxのbuild

nginx内に移動

```bash
$ cd nginx
$ docker build -t my_nginx .
```

#### php-fpmのbuild
php-fpm内に移動

```bash
$ cd ../php-fpm
$ docker build -t my_php-fpm .
```

#### mysqlのbuild
mysql内に移動

```bash
$ cd ../mysql
$ docker build -t my_mysql .
```

#### memcachedのbuild
memcached内に移動

```bash
$ cd ../memcached
$ docker build -t my_memcached .
```

### コンテナの立ち上げ

**作業ディレクトリ:docker_lemp**

```bash
$ docker-compose up -d
```