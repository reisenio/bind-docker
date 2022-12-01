FROM debian:latest

LABEL maintainer="jcgaliana@gmail.com"

ENV BIND_USER=bind \
    DATA_DIR=/data

RUN rm -rf /etc/apt/apt.conf.d/docker-gzip-indexes \
 && apt-get update \
 && apt-get upgrade -y \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y \
      bind9 bind9-host dnsutils \
 && rm -rf /var/lib/apt/lists/*

COPY entrypoint.sh /sbin/entrypoint.sh

RUN chmod 755 /sbin/entrypoint.sh

EXPOSE 53/udp 53/tcp

COPY named.conf.local /etc/bind/named.conf.local
COPY named.conf.options /etc/bind/named.conf.options
COPY rndc.key /etc/bind/rndc.key

ENTRYPOINT ["/sbin/entrypoint.sh"]

CMD ["/usr/sbin/named"]
