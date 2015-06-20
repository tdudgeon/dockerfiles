# Dockerfile for Lazar OpenTox servcies
# There are lots of issues with this Dockerfile that need to be resolved.
# Right now we focus on getting a functional build.

FROM debian:wheezy
MAINTAINER Tim Dudgeon <tdudgeon@informaticsmatters.com>

# note: password should be changed if you want a secure setup
RUN useradd -p $(openssl passwd -1 opentox) -m -s /bin/bash -G sudo opentox
# avoid password prompt for sudo
RUN sh -c 'echo "\nopentox ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers'

RUN apt-get update && apt-get install -y\
 openssl\
 git\
 sudo\
 aptitude\
 wget\
 automake\
 avahi-daemon\
 build-essential\
 cmake\
 curl\
 gnuplot\
 inetutils-syslogd\
 libavahi-glib-dev\
 libavahi-client-dev\
 libcairo2-dev\
 libglib2.0-dev\
 libgsl0-dev\
 libopenssl-ruby\
 libpcre3-dev\
 libraptor2-dev\
 libreadline-dev\
 libssl-dev\
 libtool\
 libxml2-dev\
 libyaml-dev\
 libqtwebkit-dev\
 libncurses5-dev\
 openjdk-6-jdk\
 r-base-dev\
 r-base\
 uuid-dev\
 xsltproc\
 xvfb\
 libruby\
 bundler


USER opentox
WORKDIR /home/opentox
COPY cache_date cache_date

RUN git clone -b development --single-branch https://github.com/opentox/install.git
WORKDIR install
RUN ./install silent
RUN bash service_install.sh

# cleanup
USER root
RUN sed -i "/opentox ALL=(ALL) NOPASSWD: ALL/d" /etc/sudoers
RUN deluser opentox sudo




