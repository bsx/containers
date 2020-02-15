FROM debian:buster-slim
LABEL description="OwnTracks Recorder"
LABEL authors="Bernd Stolle <bsx@0xcafec0.de>"

ADD http://repo.owntracks.org/repo.owntracks.org.gpg.key /tmp/owntracks.gpg.key

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y gnupg && \
    apt-key add /tmp/owntracks.gpg.key && \
    apt-get update && \
    echo 'deb http://repo.owntracks.org/debian stretch main' > /etc/apt/sources.list.d/owntracks.list && \
    apt-get update && \
    apt-get install -y \
        ot-recorder \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# data volume
VOLUME /owntracks

COPY ot-recorder.default /etc/default/ot-recorder

COPY launcher.sh /usr/local/sbin/launcher.sh

RUN mkdir -p /var/log/supervisor && \
    mkdir -p -m 775 /owntracks/recorder/store && \
    chown -R owntracks:owntracks /owntracks && \
    chmod 755 /usr/local/sbin/launcher.sh

EXPOSE 8083
CMD ["/usr/local/sbin/launcher.sh"]
