FROM gcr.io/google-appengine/debian9
ENV PUSHGATEWAY_VERSION 0.5.1

ENV PUSHGATEWAY_URL="https://github.com/prometheus/pushgateway/releases/download/v$PUSHGATEWAY_VERSION/pushgateway-$PUSHGATEWAY_VERSION.linux-amd64.tar.gz"
ENV PUSHGATEWAY_SHA256 99ad40f6b38a6e5a6504bf3ed593900eaa5713cc166a74e6d8c16ed6029a0435

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
