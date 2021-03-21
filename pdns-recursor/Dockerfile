FROM alpine:latest
LABEL maintainer="bsx <bsx+docker@0xcafec0.de>"

RUN apk add --no-cache pdns-recursor

VOLUME /etc/pdns

COPY recursor.conf /etc/pdns/recursor.conf

RUN mkdir -p /var/run/pdns-recursor

EXPOSE 53/tcp 53/udp

ENTRYPOINT ["/usr/sbin/pdns_recursor"]
