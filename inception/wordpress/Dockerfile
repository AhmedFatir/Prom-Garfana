FROM debian:bullseye

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y curl php php7.4-fpm php-mysql mariadb-client mycli \
    && rm -rf /var/lib/apt/lists/*

COPY /conf/wp_conf.sh /

RUN  chmod +x wp_conf.sh

ENTRYPOINT ["./wp_conf.sh"]