# Dockerfile for RDKit and PostgreSQL cartridge

FROM ubuntu:trusty
MAINTAINER Tim Dudgeon <tdudgeon@informaticsmatters.com>

# Add the PostgreSQL PGP key to verify their Debian packages.
# It should be the same key as https://www.postgresql.org/media/keys/ACCC4CF8.asc
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8

# Add PostgreSQL's repository for 9.4. 
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main 9.4" > /etc/apt/sources.list.d/pgdg.list

# Install PostgreSQL 9.4
#  There are some warnings (in red) that show up during the build. You can hide
#  them by prefixing each apt-get statement with DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
 postgresql-9.4\
 postgresql-client-9.4\
 postgresql-contrib-9.4\
 postgresql-server-dev-9.4\
 wget\
 flex\
 bison\
 build-essential\
 python-numpy\
 cmake\
 python-dev\
 sqlite3\
 libsqlite3-dev\
 libboost-dev\
 libboost-python-dev\
 libboost-regex-dev\
 libboost-all-dev

# Note: The official Debian and Ubuntu images automatically ``apt-get clean``
# after each ``apt-get``

# RDKit stuff
RUN wget http://downloads.sourceforge.net/project/rdkit/rdkit/Q1_2015/RDKit_2015_03_1.tgz
RUN gunzip -c RDKit_2015_03_1.tar.gz | tar xv
RUN rm RDKit_2015_03_1.tar.gz
ENV \
 RDBASE=/rdkit-Release_2015_03_1\
 LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$RDBASE:/usr/lib/x86_64-linux-gnu/\
 PYTHONPATH=$PYTHONPATH:$RDBASE

RUN mkdir $RDBASE/build
WORKDIR $RDBASE/build
RUN cmake .. && make && make install 


# Run the rest of the commands as the ``postgres`` user created by the ``postgres-9.4`` package when it was ``apt-get installed``
USER postgres

# Create a PostgreSQL role named ``docker`` with ``docker`` as the password and
# then create a database `docker` owned by the ``docker`` role.
# Note: here we use ``&&\`` to run commands one after the other - the ``\``
#       allows the RUN command to span multiple lines.
RUN    /etc/init.d/postgresql start &&\
    psql --command "CREATE USER docker WITH SUPERUSER PASSWORD 'docker';" &&\
    createdb -O docker docker

# Adjust PostgreSQL configuration so that remote connections to the
# database are possible. 
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.4/main/pg_hba.conf

# And add ``listen_addresses`` to ``/etc/postgresql/9.4/main/postgresql.conf``
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.4/main/postgresql.conf

# Expose the PostgreSQL port
EXPOSE 5432

# Add VOLUMEs to allow backup of config, logs and databases
VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

# Set the default command to run when starting the container
CMD ["/usr/lib/postgresql/9.4/bin/postgres", "-D", "/var/lib/postgresql/9.4/main", "-c", "config_file=/etc/postgresql/9.4/main/postgresql.conf"]
