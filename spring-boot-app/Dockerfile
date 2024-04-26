# If using ARM architecture download this the according platform version of the maven image
# separately before running the docker-compose
FROM maven:3.8.6-jdk-8 as builder

WORKDIR /app

RUN apt-get update && apt-get install -y git
RUN git clone https://github.com/kkenan/basic-microservices.git

WORKDIR /app/basic-microservices/spring-boot-app

# Not best practice but easiest and most straight-forward solution, imo better than host network_mode
RUN sed -i 's/localhost:5432/db:5432/g' ./src/main/resources/application.yml
RUN sed -i 's/localhost:8081/node-app:8081/g' ./src/main/resources/application.yml

RUN mvn clean package

FROM openjdk:8-jre-slim

WORKDIR /app

COPY --from=builder /app/basic-microservices/spring-boot-app/target/*.jar /app/app.jar

EXPOSE 8080

CMD ["java", "-jar", "/app/app.jar"]
