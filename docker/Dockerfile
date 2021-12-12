FROM ubuntu:focal

LABEL maintainer="elgeeko"

# install latest dnscrypt-proxy
# gnupg2 is needed by apt-key add
# ca-certificates is used by dnscrypt-proxy to verify resolvers
RUN apt-get update -q \
  && apt-get install --no-install-recommends -y -q \
    gnupg2 \
    ca-certificates \
  && apt-key adv --keyserver keyserver.ubuntu.com --recv-key EEE1EE950DF627C6879627B56C46343FA0B41DB7 \
  && echo deb http://ppa.launchpad.net/shevchuk/dnscrypt-proxy/ubuntu focal main >> /etc/apt/sources.list \
  && echo deb-src http://ppa.launchpad.net/shevchuk/dnscrypt-proxy/ubuntu focal main >> /etc/apt/sources.list \
  && apt-get update -q \
  && apt-get install --no-install-recommends --upgrade -y -q \
    net-tools \
    dnscrypt-proxy \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

# configure filesystem
RUN adduser --disabled-password --gecos "" --shell /bin/bash dnscrypt \
  && mkdir -p /etc/dnscrypt-proxy \
  && chown -R dnscrypt:dnscrypt /etc/dnscrypt-proxy \
  && mkdir -p /var/cache/dnscrypt-proxy \
  && chown -R dnscrypt:dnscrypt /var/cache/dnscrypt-proxy
# persistent cache
VOLUME ["/var/cache/dnscrypt-proxy"]

USER ${CONTAINER_USER}

USER dnscrypt
WORKDIR /etc/dnscrypt-proxy

ENTRYPOINT dnscrypt-proxy -config /etc/dnscrypt-proxy/dnscrypt-proxy.toml

HEALTHCHECK --interval=1m --timeout=10s --start-period=10s \
   CMD dnscrypt-proxy -config /etc/dnscrypt-proxy/dnscrypt-proxy.toml -resolve example.com
