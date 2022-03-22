# Docker-examen
Este trabajo consiste en dockerizar el examen que hicimos en Java (https://github.com/AndreuSorell/Galley-grub).

Para ello he utilizado este Dockerfile:
```
FROM maven:3.8.4-openjdk-11-slim AS build

WORKDIR /home/app

COPY src src
COPY pom.xml pom.xml
RUN mvn -f /home/app/pom.xml clean package -q

FROM openjdk:11.0-jre-slim-buster

LABEL "edu.poniperro.galleygrub.galleygrub"="galleygrub"
LABEL version=1.0-SNAPSHOT
LABEL mantainer="asorellpou@cifpfbmoll.eu"

COPY --from=build /home/app/target/galleygrub-1.0-SNAPSHOT.jar /usr/local/lib/galleygrub.jar
CMD ["java","-jar","/usr/local/lib/galleygrub.jar"]
```
Donde declaro la imagen base en el ```FROM``` , etc
