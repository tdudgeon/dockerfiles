FROM java:openjdk-8-jre
MAINTAINER tdudgeon@informaticsmatters.com


RUN apt-get update && apt-get install -y python2.7 python-numpy bzip2
RUN wget -O jython-installer-2.7.0.jar http://search.maven.org/remotecontent?filepath=org/python/jython-installer/2.7.0/jython-installer-2.7.0.jar
RUN mkdir JyNI
RUN mkdir JyNI/lib
RUN mkdir JyNI/src
WORKDIR JyNI
RUN wget -O JyNI-2.7-alpha.2.3.jar https://github.com/Stewori/JyNI/releases/download/v2.7-alpha.2.3/JyNI-2.7-alpha.2.3.jar
RUN wget -O lib/JyNI-2.7-alpha.2.3-bin-64.tar.bz2 https://github.com/Stewori/JyNI/releases/download/v2.7-alpha.2.3/JyNI-2.7-alpha.2.3-bin-64.tar.bz2
RUN wget -O src/v2.7-alpha.2.3.tar.gz https://github.com/Stewori/JyNI/archive/v2.7-alpha.2.3.tar.gz
WORKDIR /JyNI/lib
RUN tar xvfj JyNI-2.7-alpha.2.3-bin-64.tar.bz2
RUN rm JyNI-2.7-alpha.2.3-bin-64.tar.bz2
WORKDIR /JyNI/src
RUN tar xvfz v2.7-alpha.2.3.tar.gz
RUN rm v2.7-alpha.2.3.tar.gz

WORKDIR /
RUN java -jar jython-installer-2.7.0.jar -s -d jython
RUN rm jython-installer-2.7.0.jar

ENV PATH "$PATH:/jython/bin"



