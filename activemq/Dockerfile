FROM java:8-jre
MAINTAINER Tim Dudgeon <tdudgeon@Informaticsmatters.com>

RUN apt-get update

ENV AMQ_VERSION="5.11.1"

RUN wget -q ftp://ftp.mirrorservice.org/sites/ftp.apache.org/activemq/${AMQ_VERSION}/apache-activemq-${AMQ_VERSION}-bin.tar.gz
RUN tar zxf apache-activemq-${AMQ_VERSION}-bin.tar.gz
RUN rm apache-activemq-${AMQ_VERSION}-bin.tar.gz


EXPOSE 8161 
EXPOSE 61616 
EXPOSE 5672
EXPOSE 61613
EXPOSE 1883 
EXPOSE 61614

CMD /apache-activemq-${AMQ_VERSION}/bin/activemq console













