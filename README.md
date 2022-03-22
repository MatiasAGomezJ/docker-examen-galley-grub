# Docker examen Galley Grub
## Trabajo creado por [Matias Gomez](https://github.com/MatiasAGomezJ)

Primero crearemos el archivo `Dockerfile` con la siguiente información.
```Dockerfile
FROM maven:3.8.4-openjdk-11-slim AS build

WORKDIR /home/app

COPY src src
COPY pom.xml pom.xml
RUN mvn -f /home/app/pom.xml clean package -q

FROM openjdk:11.0-jre-slim-buster

LABEL "edu.poniperro.galleygrub"="galleygrub"
LABEL version=1.0-SNAPSHOT

COPY --from=build /home/app/target/GalleyGrub-1.0-SNAPSHOT.jar /usr/local/lib/galleygrub.jar
CMD ["java","-jar","/usr/local/lib/galleygrub.jar"]
```
![image](https://user-images.githubusercontent.com/91556480/159595008-24ddbed5-813a-48ca-9df5-6fa090d84404.png)

Hecho esto construiremos la imagen:
```bash
$ docker built -t galleygrub .
```
![image](https://user-images.githubusercontent.com/91556480/159595194-a1bc7bf7-0111-4a16-b33a-59d8e2762529.png)

Para acabar ejecutaremos la imagen:
```bash
$ docker run galleygrub
```
![image](https://user-images.githubusercontent.com/91556480/159595336-4663fd50-1215-439b-a717-d9c5337155e9.png)
