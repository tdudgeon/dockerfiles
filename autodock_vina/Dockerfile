# Dockerfile for autodock vina
# autodock vina is nothing to do with docker. It's a molecular docking program.
# See here for details: http://vina.scripps.edu/index.html

FROM ubuntu:14.04
MAINTAINER Tim Dudgeon <tdudgeon@informaticsmatters.com>

RUN apt-get update && apt-get install -y wget
RUN wget http://vina.scripps.edu/download/autodock_vina_1_1_2_linux_x86.tgz
RUN gunzip autodock_vina_1_1_2_linux_x86.tgz
RUN tar xvf autodock_vina_1_1_2_linux_x86.tar
RUN rm autodock_vina_1_1_2_linux_x86.tar
RUN sudo cp autodock_vina_1_1_2_linux_x86/bin/* /usr/local/bin
