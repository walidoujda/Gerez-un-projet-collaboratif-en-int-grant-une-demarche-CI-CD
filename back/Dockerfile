# Étape de construction
FROM openjdk:11 as build

# Installer Maven
RUN apt-get update && apt-get install -y maven

# Copier uniquement le fichier pom.xml d'abord pour utiliser le cache Docker efficacement
COPY pom.xml .

# Télécharger les dépendances Maven pour les cacher (sauf si pom.xml change)
RUN mvn dependency:go-offline

# Copier les sources seulement après les dépendances pour éviter de les re-télécharger si seul le code source change
COPY src/ src/

# Construire l'application sans exécuter les tests pour accélérer le build
RUN mvn clean install -DskipTests

# Étape de runtime
FROM openjdk:11-jre-slim

# Définir le répertoire de travail
WORKDIR /bobapp

# Copier l'artefact construit depuis l'étape de build
COPY --from=build /target/*.jar bobapp.jar

# Définir la commande pour exécuter l'application
ENTRYPOINT ["java", "-jar", "bobapp.jar"]
