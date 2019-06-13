FROM maven:3-jdk-8

ENV PARAMS=""

RUN wget https://codeload.github.com/xuxueli/xxl-job/zip/master
RUN mkdir /source
RUN unzip master -d /source
WORKDIR /source/xxl-job-master
RUN mvn clean package -Dmaven.test.skip=true

FROM openjdk:8-jre
LABEL maintainer="conf"
COPY --from=0 /source/xxl-job-master/xxl-conf-admin/target/xxl-job-admin-*.jar /app.jar
ENTRYPOINT ["sh","-c","java -jar /app.jar $PARAMS"]
EXPOSE 8080
