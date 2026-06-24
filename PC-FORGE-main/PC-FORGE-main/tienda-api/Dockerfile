# --- Fase 1: Compilación ---
# Cambiamos a una imagen de Maven que use Eclipse Temurin para Java 17
FROM maven:3.8.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# --- Fase 2: Ejecución ---
# Cambiamos la imagen obsoleta openjdk por Amazon Corretto 17 (Estable y ligera)
FROM amazoncorretto:17-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]