FROM ubuntu:cosmic
MAINTAINER Chris Buckley <cbuckleysa@gmail.com>

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get dist-upgrade -y \
  && DEBIAN_FRONTEND=noninteractive apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    git \
    golang \
    wget

RUN mkdir /opt/ll-app \
  && mkdir /opt/gocache

COPY . /opt/ll-app

WORKDIR /opt/ll-app

ENV GOPATH /opt/gopath
ENV GOCACHE /opt/gocache

RUN go get -d -v . \
  && go build \
  && go get -d -v . \
  && go build \
  && rm -r -f www logs \
  && mkdir www logs \
  && chown -R nobody /opt/gocache www

RUN DEBIAN_FRONTEND=noninteractive apt-get remove -y \
  git \
  wget \
  && DEBIAN_FRONTEND=noninteractive apt-get -y autoclean \
  && DEBIAN_FRONTEND=noninteractive apt-get -y autoremove \
  && rm -rf /var/lib/apt/lists/*

USER nobody

EXPOSE 8080

CMD go run main.go "./www" 1> /dev/stdout 2>&1




