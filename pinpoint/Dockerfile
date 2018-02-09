FROM debian:jessie
MAINTAINER diegoazd <diegoazd@gmail.com>

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
  apt-utils \
  curl \
  git \
  net-tools \
  procps \
  software-properties-common \
  wget \
  unzip \
  zip

RUN curl -s "https://get.sdkman.io" | bash 

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN source "/root/.sdkman/bin/sdkman-init.sh" && echo 'n' | sdk install java 6u93-zulu && echo 'n' | sdk install java 7u141-zulu && echo 'n' | sdk install java 8u152-zulu

ENV JAVA_6_HOME  /root/.sdkman/candidates/java/6u93-zulu
ENV JAVA_7_HOME /root/.sdkman/candidates/java/7u141-zulu
ENV JAVA_8_HOME /root/.sdkman/candidates/java/8u152-zulu
ENV JAVA_HOME /root/.sdkman/candidates/java/8u152-zulu

RUN useradd pinpoint -m

WORKDIR /usr/local/apache-maven
ADD https://archive.apache.org/dist/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz ./
ADD https://archive.apache.org/dist/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz.sha1 ./
RUN [ $(sha1sum apache-maven-3.2.5-bin.tar.gz | grep --only-matching -m 1 '^[0-9a-f]*') = $(cat apache-maven-3.2.5-bin.tar.gz.sha1) ]
RUN tar -xf apache-maven-3.2.5-bin.tar.gz
ENV PATH $PATH:/usr/local/apache-maven/apache-maven-3.2.5/bin
RUN rm apache-maven-3.2.5-bin.tar.gz apache-maven-3.2.5-bin.tar.gz.sha1

WORKDIR /
RUN git clone https://github.com/naver/pinpoint.git
WORKDIR /pinpoint
RUN mvn install -Dmaven.test.skip=true -B

WORKDIR quickstart/hbase
ADD https://archive.apache.org/dist/hbase/hbase-1.0.3/hbase-1.0.3-bin.tar.gz ./
RUN tar -xf hbase-1.0.3-bin.tar.gz
RUN rm hbase-1.0.3-bin.tar.gz
RUN ln -s hbase-1.0.3 hbase

WORKDIR /pinpoint
VOLUME [/pinpoint]
