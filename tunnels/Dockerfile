FROM alpine:edge

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

ADD https://github.com/just-containers/s6-overlay/releases/download/v2.2.0.1/s6-overlay-amd64-installer /tmp/
RUN chmod +x /tmp/s6-overlay-amd64-installer && /tmp/s6-overlay-amd64-installer / && \
    apk add --no-cache wireguard-tools iproute2 && \
    apk add --no-cache --virtual .build-deps go make git && \
    git clone https://hub.fastgit.org/WireGuard/wireguard-go.git && \
    cd wireguard-go && make && make install && \
    cd .. && rm -rf wireguard-go && apk del .build-deps

COPY ./root /

ENTRYPOINT ["/init"]
