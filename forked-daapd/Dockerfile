FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_PRIORITY critical
ENV DEBCONF_NOWARNINGS yes

RUN echo 'Acquire::http { Proxy "http://172.17.42.1:3128"; };' >> /etc/apt/apt.conf.d/01proxy
RUN echo 'Acquire::http::User-Agent "Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.1; Trident/6.0)";' >> /etc/apt/apt.conf.d/01proxy
 
RUN apt-get -y update && apt-get install -y ruby forked-daapd && \
          rm -Rf /var/lib/apt/lists/*

VOLUME /media
ADD forked-daapd.conf.erb /etc/forked-daapd.conf.erb
ADD start /usr/sbin/start

EXPOSE 3689

CMD ["bash", "/usr/sbin/start"]

