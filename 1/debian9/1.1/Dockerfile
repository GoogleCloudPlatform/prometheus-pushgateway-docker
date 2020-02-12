FROM gcr.io/google-appengine/debian9
ENV PUSHGATEWAY_VERSION 1.1.0

ENV C2D_RELEASE=${PUSHGATEWAY_VERSION}

ENV PUSHGATEWAY_URL="https://github.com/prometheus/pushgateway/releases/download/v$PUSHGATEWAY_VERSION/pushgateway-$PUSHGATEWAY_VERSION.linux-amd64.tar.gz"
ENV PUSHGATEWAY_SHA256 fef0230e9ac336585c5b7b032bbc16879dee47f22995c45640064e64f8fbaa2a

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
