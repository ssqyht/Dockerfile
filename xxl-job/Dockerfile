FROM openjdk:8-jdk
RUN mkdir /source && git clone https://github.com/xuxueli/xxl-job
WORKDIR /source
RUN ./mvnw clean package -Dmaven.test.skip=true

FROM openjdk:8-jre
COPY --from=0 /source/xxl-job/xxl-job-admin/target/xxl-job-admin-*.jar  /app.jar
ENTRYPOINT ["java","-XX:+UnlockExperimentalVMOptions","-XX:+UseCGroupMemoryLimitForHeap","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
EXPOSE 8080
