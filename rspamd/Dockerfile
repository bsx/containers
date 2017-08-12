FROM debian:stretch-slim
LABEL maintainer="bsx <bsx+docker@0xcafec0.de>"

ENV DEBIAN_FRONTEND=noninteractive LC_ALL=C

RUN apt-get update \
    && apt-get install -y ca-certificates gnupg2 apt-transport-https \
    && apt-key adv --fetch-keys https://rspamd.com/apt-stable/gpg.key \
    && echo "deb https://rspamd.com/apt-stable/ stretch main" > /etc/apt/sources.list.d/rspamd.list \
    && apt-get update && apt-get install -y rspamd \
    && echo 'type = "console"' >> /etc/rspamd/local.d/logging.inc \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get autoremove --purge \
    && apt-get clean \
    && mkdir -p /run/rspamd \
    && chown _rspamd:_rspamd /run/rspamd

VOLUME /etc/rspamd/local.d /etc/rspamd/override.d /var/lib/rspamd

EXPOSE 11332 11333 11334 11335

CMD ["/usr/bin/rspamd", "-f", "-u", "_rspamd", "-g", "_rspamd"]
