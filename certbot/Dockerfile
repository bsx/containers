FROM certbot/certbot:v0.21.0
LABEL maintainer="bsx <bsx+docker@0xcafec0.de>"

ENV CERTBOT_VERSION="0.21.0"

RUN pip install --no-cache-dir \
    certbot-dns-cloudflare==${CERTBOT_VERSION} \
    certbot-dns-cloudxns==${CERTBOT_VERSION} \
    certbot-dns-digitalocean==${CERTBOT_VERSION} \
    certbot-dns-dnsimple==${CERTBOT_VERSION} \
    certbot-dns-dnsmadeeasy==${CERTBOT_VERSION} \
    certbot-dns-google==${CERTBOT_VERSION} \
    certbot-dns-luadns==${CERTBOT_VERSION} \
    certbot-dns-nsone==${CERTBOT_VERSION} \
    certbot-dns-rfc2136==${CERTBOT_VERSION} \
    certbot-dns-route53==${CERTBOT_VERSION}
