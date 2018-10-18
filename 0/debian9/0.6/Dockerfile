FROM gcr.io/google-appengine/debian9
ENV PUSHGATEWAY_VERSION 0.6.0

ENV PUSHGATEWAY_URL="https://github.com/prometheus/pushgateway/releases/download/v$PUSHGATEWAY_VERSION/pushgateway-$PUSHGATEWAY_VERSION.linux-amd64.tar.gz"
ENV PUSHGATEWAY_SHA256 f264fe51ff904f648656ce2cdca4256878de307f40c61d51eb8700aae94390ce

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
