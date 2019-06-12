FROM openjdk:8-jdk

ENV PARAMS=""

RUN wget http://apache-mirror.rbc.ru/pub/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
RUN tar xzvf apache-maven-3.3.9-bin.tar.gz
RUN cp -R apache-maven-3.3.9 /usr/local/bin
RUN export PATH=apache-maven-3.3.9/bin:$PATH
RUN export PATH=/usr/local/bin/apache-maven-3.3.9/bin:$PATH
RUN ln -s /usr/local/bin/apache-maven-3.3.9/bin/mvn /usr/local/bin/mvn
#RUN ls -l /usr/local/bin
RUN echo $PATH

RUN mkdir /source && wget https://gitee.com/xuxueli0323/xxl-conf/repository/archive/master.zip && unzip master.zip -d /source
WORKDIR /source/xxl-conf
RUN mvn clean package -Dmaven.test.skip=true

FROM openjdk:8-jre
LABEL maintainer="conf"
COPY --from=0 /source/xxl-conf/xxl-conf-admin/target/xxl-conf-admin-*.jar /app.jar
ENTRYPOINT ["sh","-c","java -jar /app.jar $PARAMS"]
EXPOSE 8080
