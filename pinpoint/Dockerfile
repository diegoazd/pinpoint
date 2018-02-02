FROM diegoazd/java-base
MAINTAINER diegoazd <diegoazd@gmail.com>

RUN useradd pinpoint -m

WORKDIR /usr/local/apache-maven
ADD https://archive.apache.org/dist/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz ./
ADD https://archive.apache.org/dist/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz.sha1 ./
RUN [ $(sha1sum apache-maven-3.2.5-bin.tar.gz | grep --only-matching -m 1 '^[0-9a-f]*') = $(cat apache-maven-3.2.5-bin.tar.gz.sha1) ]
RUN tar -xf apache-maven-3.2.5-bin.tar.gz
ENV PATH $PATH:/usr/local/apache-maven/apache-maven-3.2.5/bin
RUN rm apache-maven-3.2.5-bin.tar.gz apache-maven-3.2.5-bin.tar.gz.sha1

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
