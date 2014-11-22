FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_PRIORITY critical
ENV DEBCONF_NOWARNINGS yes

RUN echo 'Acquire::http { Proxy "http://172.17.42.1:3128"; };' >> /etc/apt/apt.conf.d/01proxy
RUN echo 'Acquire::http::User-Agent "Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.1; Trident/6.0)";' >> /etc/apt/apt.conf.d/01proxy
RUN echo 'deb-src http://ftp.us.debian.org/debian/ jessie main contrib non-free' >> /etc/apt/sources.list
 
RUN apt-get -y update && apt-get install -y curl ruby && \
      apt-get -y build-dep minidlna && \
          cd /tmp && \
          bash -c "curl -x http://172.17.42.1:3128 -L 'http://downloads.sourceforge.net/project/minidlna/minidlna/1.1.4/minidlna-1.1.4.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fminidlna%2F&ts=1416445930&use_mirror=softlayer-dal' | tar zxvf -" && \
          cd minidlna-1.1.4 && \
          ./configure && \
          make -j3 && \
          make install && \
          cd .. && \
          rm -Rf minidlna-1.1.4 && \
          dpkg -l | grep -- "-dev" | awk '{print $2}' | xargs apt-get -y remove && \
          rm -Rf /var/lib/apt/lists/*

VOLUME /media
ADD minidlna.conf.erb /etc/minidlna.conf.erb
ADD start /usr/sbin/start

EXPOSE 1900/udp
EXPOSE 8200

CMD ["bash", "/usr/sbin/start"]

