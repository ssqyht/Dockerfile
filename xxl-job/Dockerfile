FROM centos:centos6
USER root

#UTILITIES
RUN     yum install -y wget
RUN     yum install -y tar
RUN     yum install -y git

RUN mkdir -p /root/workspace
WORKDIR /root/workspace

RUN unset SSH_ASKPASS
RUN git clone --depth=1 https://github.com/xuxueli/xxl-job
WORKDIR /root/workspace/xxl-job

#JAVA (OPENJDK 7)
ENV JAVA_VERSION 1.7.0

RUN yum install -y java-1.7.0-openjdk java-1.7.0-openjdk-devel

ENV JAVA_HOME /usr/lib/jvm/java

ENV TZ=PRC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN wget http://apache-mirror.rbc.ru/pub/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
RUN tar xzvf apache-maven-3.3.9-bin.tar.gz
RUN cp -R apache-maven-3.3.9 /usr/local/bin
RUN export PATH=apache-maven-3.3.9/bin:$PATH
RUN export PATH=/usr/local/bin/apache-maven-3.3.9/bin:$PATH
RUN ln -s /usr/local/bin/apache-maven-3.3.9/bin/mvn /usr/local/bin/mvn
#RUN ls -l /usr/local/bin
RUN echo $PATH

RUN set -ex && mvn clean install -DskipTests

ADD xxl-job-admin/target/xxl-job-admin-*.jar /app.jar

ENTRYPOINT ["sh","-c","java -jar /app.jar $PARAMS"]
