##
## Runner
##
FROM ubuntu:20.04

WORKDIR /opt/rtpengine

RUN apt-get update 
#RUN apt-get upgrade
# RUN apt-get -y dist-upgrade 


RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC  apt-get install -y build-essential git  libglib2.0-dev libavcodec-dev \
	zlib1g-dev pkgconf perl gperf libssl-dev libevent-dev libpcap-dev libspandsp-dev \
	libhiredis-dev libxmlrpc-core-c3-dev libmariadb-dev cmake libwebsockets-dev libavformat-dev \
	libjson-glib-dev libavfilter-dev libcurl4-nss-dev libmariadb-dev-compat gettext-base \
	libnftnl-dev libmnl-dev libopus-dev pandoc iptables libncurses-dev kmod 

RUN git clone https://github.com/sipwise/rtpengine.git

RUN cd rtpengine  && with_iptables_option=no make && make install

RUN  apt-get -y install linux-headers-$(uname -r) linux-image-$(uname -r)

RUN cd rtpengine/kernel-module/ && make && make install

#RUN rm -rf /opt/rtpengine/*

RUN groupadd -r rtpengine && useradd -r -g rtpengine rtpengine

COPY ./entrypoint.sh /opt/rtpengine/entrypoint.sh
COPY ./rtpengine.conf /opt/rtpengine/rtpengine.conf
COPY ./rtpengine-recording.conf /opt/rtpengine/rtpengine-recording.conf

RUN mkdir -p /tmp/metadata
RUN mkdir -p /tmp/rtpengine-recording

RUN chown -R rtpengine:rtpengine /tmp/metadata
RUN chown -R rtpengine:rtpengine /tmp/rtpengine-recording

RUN chown -R rtpengine:rtpengine .

RUN chmod +x entrypoint.sh

USER rtpengine

ENTRYPOINT ["/opt/rtpengine/entrypoint.sh"]
CMD ["rtpengine"]