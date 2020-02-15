FROM alpine:3.11
LABEL maintainer="bsx <bsx+docker@0xcafec0.de>"

RUN apk add --no-cache pdns-recursor

VOLUME /etc/pdns

COPY recursor.conf /etc/pdns/recursor.conf

EXPOSE 53/tcp 53/udp

ENTRYPOINT ["/usr/sbin/pdns_recursor"]
