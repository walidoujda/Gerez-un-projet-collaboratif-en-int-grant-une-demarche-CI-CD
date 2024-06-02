# Étape de construction
FROM maven:3.8.4-openjdk-17-slim AS build

WORKDIR /app

COPY pom.xml .
COPY src ./src
RUN mvn clean package 

# Étape de production
FROM openjdk:20-slim

# Remplacez 'app.jar' par le nom exact du fichier jar produit par Maven
COPY --from=build /app/target/*.jar /app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app.jar"]
