FROM ubuntu

MAINTAINER Prangya P Kar "prangya.kar@gmail.com"

ARG enable_telemetry="false"

#install required software in ubuntu container

RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y git
RUN rm -rf /var/lib/apt/lists/*

#install go , latest version as of 25 February 2020
#https://blog.golang.org/go1.14

ENV GOLANG_VERSION 1.14
RUN curl -sSL https://storage.googleapis.com/golang/go$GOLANG_VERSION.linux-amd64.tar.gz \
		| tar -v -C /usr/local -xz

ENV PATH /usr/local/go/bin:$PATH
RUN mkdir -p /go/src /go/bin && chmod -R 777 /go
ENV GOROOT /usr/local/go
ENV GOPATH /go
ENV PATH /go/bin:$PATH
WORKDIR /go
RUN git version
RUN go version
RUN go env
RUN which go
WORKDIR $GOPATH/src
RUN echo "$PWD"
RUN export GO111MODULE=on

#install caddy

RUN git clone -b v2 "https://github.com/caddyserver/caddy.git"


RUN echo "$PWD"
WORKDIR caddy/cmd/caddy/
RUN ls -la
#build caddy
RUN go build

# Telemetry Stats
ENV ENABLE_TELEMETRY="$enable_telemetry"

#expose port 8080 of container
EXPOSE 8080

#validate install
RUN ./caddy version
COPY Caddyfile /etc/Caddyfile


ENTRYPOINT /go/src/caddy/cmd/caddy/caddy run --config /etc/Caddyfile --adapter caddyfile

#ref:
#docker build -t prangya-caddy-image:1.0 . -f Dockerfile --no-cache
#docker run -it --name prangya-caddy-web -p 8080:8080 prangya-caddy-image:1.0

#https://github.com/caddyserver/caddy/tree/v2#build-from-source
#https://caddyserver.com/docs/install
#https://www.linode.com/docs/development/go/install-go-on-ubuntu/
