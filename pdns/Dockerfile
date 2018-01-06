FROM alpine:3.7
LABEL maintainer="bsx <bsx+docker@0xcafec0.de>"

RUN apk add --no-cache pdns pdns-backend-pgsql

COPY pdns.conf /etc/pdns/pdns.conf

VOLUME /etc/pdns

EXPOSE 53/tcp 53/udp

ENTRYPOINT ["/usr/sbin/pdns_server"]
