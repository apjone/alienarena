FROM ubuntu:22.04
RUN echo 'APT::Install-Suggests "0";' >> /etc/apt/apt.conf.d/00-docker
RUN echo 'APT::Install-Recommends "0";' >> /etc/apt/apt.conf.d/00-docker
RUN DEBIAN_FRONTEND=noninteractive \
  apt-get update \
  && apt-get install -y sharutils libglu1-mesa-dev libgl1-mesa-dev libjpeg-dev libpng-dev libxxf86vm-dev libxxf86dga-dev libxext-dev libx11-dev libcurl4-gnutls-dev libopenal-dev libvorbis-dev libfreetype6-dev pkg-config wget build-essential screen\
  && rm -rf /var/lib/apt/lists/*
ADD https://github.com/apjone/alienarena/archive/refs/tags/latest.tar.gz /tmp/latest.tar.gz
RUN tar zxvf /tmp/latest.tar.gz
RUN rm /tmp/latest.tar.gz
RUN cd /alienarena-latest && ./configure --disable-client && make && make install 
RUN rm -rf /alienarena-latest
RUN useradd -ms /bin/bash alien
RUN mkdir -pv /home/alien/.local/share/cor-games
RUN chown -R alien. /home/alien/.local
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
USER alien
WORKDIR /home/alien
ENV COR_GAMES=.local/share/cor-games
ENTRYPOINT ["/entrypoint.sh"]
EXPOSE 27910/udp
