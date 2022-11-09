FROM maven:3.6.3 AS maven_build

WORKDIR /usr/src/app
COPY . /usr/src/app

RUN ["mvn","install", "-Dmaven.test.skip=true"]

FROM openjdk:11-oracle
VOLUME /tmp
COPY --from=maven_build /usr/src/app/target/*.jar /tmp

COPY target/*.jar app.jar

ENTRYPOINT ["java", "-jar","/app.jar", "--spring.profiles.active=docker"]
