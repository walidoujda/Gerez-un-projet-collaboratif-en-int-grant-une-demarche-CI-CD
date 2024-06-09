# Utilisez l'image officielle de Maven qui inclut OpenJDK
FROM maven:3.8.4-openjdk-11 as build

# Définissez le répertoire de travail dans l'image Docker
WORKDIR /app

# Copiez vos fichiers de projet dans l'image Docker
COPY . .

# Facultatif : exécutez les commandes de résolution des dépendances pour améliorer la mise en cache des couches
RUN mvn dependency:resolve

# Construisez votre application sans exécuter les tests
RUN mvn clean install -DskipTests

# Deuxième étape pour configurer le conteneur de runtime
FROM openjdk:11-jre-slim
WORKDIR /app

# Copiez l'artefact construit de la première étape
COPY --from=build /app/target/*.jar ./app.jar

# Définissez la commande pour exécuter l'application
ENTRYPOINT ["java", "-jar", "app.jar"]
