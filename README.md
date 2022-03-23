# Docker-examen
### Este trabajo consiste en dockerizar el examen que hicimos en Java (https://github.com/AndreuSorell/Galley-grub).

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
Donde la estructura que he seguido para el Dockerfile es la siguiente:
- ```FROM``` -> declara la imagen base
- ```WORKDIR``` -> especifica la carpeta de trabajo dentro del contenedor
- ```COPY``` -> copia los ficheros
- ```RUN``` -> ejecuta el comando en el momento de la creación de la imagen
- ```LABEL``` -> Para los metadatos
- ```CMD``` -> ejecuta el comando en el momento de ejecución del contenedor

Una vez creado el Dockerfile, para crear la imagen, he lanzado el siguiente comando:
```docker build -t galleygrub .```
![image](https://user-images.githubusercontent.com/91556405/159769563-196f366e-39b8-4df5-a50a-8d827fc101c0.png)

Y finalmente con: ```docker run <nombre de la imagen>``` he podido lanzar mi app en un contenedor.
![image](https://user-images.githubusercontent.com/91556405/159770179-fdd34733-fcec-4522-af75-b635369b21ee.png)


