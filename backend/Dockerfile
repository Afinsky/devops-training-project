FROM gradle:4.7.0-jdk8-alpine AS build
COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle build --no-daemon -x test 1>/dev/null

#RUN ls -laR /home/gradle

#CMD /bin/sh

FROM openjdk:8-jre-slim

ENV "DB_USERNAME"=""
ENV "DB_PASSWORD"=""
ENV "DB_URL"=""
ENV "DB_PORT"=""
ENV "DB_NAME"=""

EXPOSE 8080

RUN mkdir /app

COPY --from=build /home/gradle/src/build/libs/*.jar /app/spring-boot-application.jar

ENTRYPOINT ["java", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-Djava.security.egd=file:/dev/./urandom","-jar","/app/spring-boot-application.jar"]
