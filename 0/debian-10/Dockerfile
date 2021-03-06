FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl gzip libc6 procps tar wget
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/nats-exporter-0.8.0-0-linux-amd64-debian-10.tar.gz && \
    echo "10d447e9201ca6bf9c0c352c1c02dae193f54a8cdc45cadbaf050256b054e371  /tmp/bitnami/pkg/cache/nats-exporter-0.8.0-0-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/nats-exporter-0.8.0-0-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/nats-exporter-0.8.0-0-linux-amd64-debian-10.tar.gz
RUN chmod g+rwX /opt/bitnami

ENV BITNAMI_APP_NAME="nats-exporter" \
    BITNAMI_IMAGE_VERSION="0.8.0-debian-10-r21" \
    PATH="/opt/bitnami/nats-exporter/bin:$PATH"

EXPOSE 7777

WORKDIR /opt/bitnami/nats-exporter
USER 1001
ENTRYPOINT [ "prometheus-nats-exporter" ]
