FROM alpine:3.11

ARG VERSION=1.3.0
ARG URL=https://github.com/mumble-voip/mumble/releases/download/${VERSION}/murmur-static_x86-${VERSION}.tar.bz2

RUN mkdir -pv /opt/mumble /etc/mumble/data

RUN adduser -DHs /sbin/nologin mumble

RUN apk add --update ca-certificates bzip2 tar tzdata wget \
    && wget -qO- ${URL} | tar -xjv --strip-components=1 -C /opt/mumble \
    && apk del ca-certificates bzip2 tar wget && rm -rf /var/cache/apk/* \
    && chown -R mumble:mumble /etc/mumble /opt/mumble

COPY murmur.ini /etc/mumble/murmur.ini

USER mumble

CMD ["/opt/mumble/murmur.x86", "-fg", "-v", "-ini", "/etc/mumble/murmur.ini"]