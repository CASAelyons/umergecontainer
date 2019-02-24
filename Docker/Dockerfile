#=========================#
#  Operating System setup #
#=========================#
from ubuntu:18.04

# install basic build environment
RUN apt-get update && \
    apt-get -y install apt-utils && \
    apt-get -y upgrade && \
    apt-get -y install gcc g++ zlib1g-dev libxml2-dev && \
    apt-get -y install curl make libnetcdf-dev libpng-dev && \
    apt-get -y install python libconfig-dev bc && \
    rm -rf /var/lib/apt/lists/*

# install libconfig in /opt/libconfig
COPY libconfig-1.5.tar.gz /opt
RUN mkdir /opt/libconfig && \
    tar xzf /opt/libconfig-1.5.tar.gz -C /opt/libconfig && \
    cd /opt/libconfig/libconfig-1.5 && \
    ./configure --prefix=/usr/local/libconfig && \
    make && make install && \
    cd /opt && \
    rm -rf /opt/libconfig && \
    rm /opt/libconfig-1.5.tar.gz
ENV LD_LIBRARY_PATH=/usr/local/libconfig/lib:$LD_LIBRARY_PATH

# install jansson in /opt/jansson
COPY jansson-2.7.tar.gz /opt
RUN mkdir /opt/jansson && \
    tar xzf /opt/jansson-2.7.tar.gz -C /opt/jansson && \
    cd /opt/jansson/jansson-2.7 && \
    ./configure --prefix=/usr/local/jansson && \
    make && make install && \
    cd /opt && \
    rm -rf /opt/jansson && \
    rm /opt/jansson-2.7.tar.gz
ENV LD_LIBRARY_PATH=/usr/local/jansson/lib:$LD_LIBRARY_PATH

# install UM_VEL
COPY UMerge_dynamo.tar /opt
RUN tar xf /opt/UMerge_dynamo.tar -C /opt && \
    cd /opt/UMerge_dynamo && make && \
    cd /opt && rm /opt/UMerge_dynamo.tar
ENV UMERGE=/opt/UMerge_dynamo
ENV PATH=/opt/UMerge_dynamo:$PATH

# install netcdf2png
COPY netcdf2png.tar /opt
RUN tar xf /opt/netcdf2png.tar -C /opt && \
    cd /opt/netcdf2png && make && \
    cd /opt && rm /opt/netcdf2png.tar
ENV PATH=/opt/netcdf2png:$PATH

