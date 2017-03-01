FROM anapsix/alpine-java:jdk7

#Original Maintainer
#MAINTAINER Jean-Marc Soumet (https://github.com/ajmssc)
MAINTAINER Koddi Inc. (https://koddi.com)

ARG ALLUXIO_VERSION=1.4.0

RUN apk add --update wget sudo supervisor openssh
RUN wget http://alluxio.org/downloads/files/${ALLUXIO_VERSION}/alluxio-${ALLUXIO_VERSION}-bin.tar.gz -O /alluxio.tar.gz && \
    tar xvzf /alluxio.tar.gz && mv /alluxio-* /alluxio && \
    rm -rf /alluxio.tar.gz


## Create ssh key
RUN mkdir -p /root/.ssh && chmod 700 /root/.ssh && ssh-keygen -A
RUN rm -f /root/.ssh/id_rsa && \
    ssh-keygen -b 2048 -t rsa -f /root/.ssh/id_rsa -q -N "" && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
    chmod og-wx ~/.ssh/authorized_keys

ENV TERM=xterm

RUN mkdir -p /dev/ram
RUN mkdir /data
ADD supervisord-*.conf /
ADD start.sh /
