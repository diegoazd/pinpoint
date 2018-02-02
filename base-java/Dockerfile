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

