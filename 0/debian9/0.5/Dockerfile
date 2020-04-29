FROM gcr.io/google-appengine/debian9
ENV PUSHGATEWAY_VERSION 0.5.2

ENV C2D_RELEASE=${PUSHGATEWAY_VERSION}

ENV PUSHGATEWAY_URL="https://github.com/prometheus/pushgateway/releases/download/v$PUSHGATEWAY_VERSION/pushgateway-$PUSHGATEWAY_VERSION.linux-amd64.tar.gz"
ENV PUSHGATEWAY_SHA256 d4aeb15b9667bae79170d4f12b4afa20dc29850aeac2ce071479d93057fb5c3b

RUN set -x && \
    apt-get update && apt-get install -qq -y wget && \
    mkdir pushgateway-files && cd pushgateway-files && \
    wget -O pushgateway.tar.gz "$PUSHGATEWAY_URL" && \
    echo "$PUSHGATEWAY_SHA256 pushgateway.tar.gz" | sha256sum -c - && \
    tar xfvz pushgateway.tar.gz --strip-components=1 && \
    mv pushgateway /bin/ && \
    mkdir -p /usr/share/doc/pushgateway && \
    mv LICENSE /usr/share/doc/pushgateway && \
    cd - && rm -r pushgateway-files && \
    mkdir -p /pushgateway

EXPOSE     9091
WORKDIR    /prometheus
ENTRYPOINT [ "/bin/pushgateway" ]
