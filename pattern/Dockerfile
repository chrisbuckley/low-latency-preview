FROM ubuntu
MAINTAINER Chris Buckley <cbuckleysa@gmail.com>

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get dist-upgrade -y \
  && DEBIAN_FRONTEND=noninteractiveRUN apt-get install -y \
    apt-utils \
    wget \
    xz-utils

WORKDIR /opt

ENV FFMPEG_VER ffmpeg-git-64bit-static

# BS trickery to keep it automated
RUN wget -q https://johnvansickle.com/ffmpeg/builds/${FFMPEG_VER}.tar.xz \
  && tar xf ${FFMPEG_VER}.tar.xz \
  && rm ${FFMPEG_VER}.tar.xz \
  && mv $(ls . | grep ffmpeg) ffmpeg

RUN DEBIAN_FRONTEND=noninteractive apt-get remove -y \
  apt-utils \
  wget \
  xz-utils \
  && DEBIAN_FRONTEND=noninteractive apt-get -y autoclean \
  && DEBIAN_FRONTEND=noninteractive apt-get -y autoremove \
  && rm -rf /var/lib/apt/lists/*

ADD launchEncoderTestPattern.sh ./
ADD utils/ /opt/utils/

ENV UTILS_DIR /opt/utils

USER nobody

CMD ./launchEncoderTestPattern.sh




