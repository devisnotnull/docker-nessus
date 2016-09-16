FROM phusion/baseimage
MAINTAINER vwieczorek
#Based on the work of Eric Schultz <eric@startuperic.com>
#Thanks to Tim Haak <tim@haak.co.uk>
ENV DEBIAN_FRONTEND noninteractive

# Set correct environment variables
ENV HOME /root

# Use baseimage-docker's init system
CMD ["/sbin/my_init"]

# chfn workaround - Known issue within Dockers
RUN ln -s -f /bin/true /usr/bin/chfn

# The Nessus directory. Where the binary, config, and database is
#RUN rm -rf /opt
VOLUME /data

# Install Nessus
RUN apt-get -q update
RUN apt-get install -qy gdebi-core wget

COPY Nessus-6.6.2.deb /tmp/

# RUN wget -O /tmp/Nessus.deb "http://downloads.nessus.org/nessus3dl.php?file=Nessus-6.4.1-debian6_amd64.deb&licence_accept=yes&t=34958f1d2820ccf2c5465e4d71ce92ff"
RUN chmod +x /tmp/Nessus-6.6.2.deb 
RUN gdebi -n /tmp/Nessus-6.6.2.deb

EXPOSE 8834

# Add nessus to runit
RUN mkdir /etc/service/nessus
RUN echo '#!/bin/bash' > /etc/service/nessus/run
RUN echo 'exec service nessusd start' >> /etc/service/nessus/run
RUN chmod +x /etc/service/nessus/run
