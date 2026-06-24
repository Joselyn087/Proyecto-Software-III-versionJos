# --- Fase 1: Compilación ---
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
# Copia el código fuente y el pom.xml
COPY pom.xml .
COPY src ./src
# Compila generando el archivo .jar omitiendo los tests para acelerar el despliegue
RUN mvn clean package -DskipTests

# --- Fase 2: Ejecución ---
FROM openjdk:17-jdk-slim
WORKDIR /app
# Copia el .jar generado desde la fase de compilación
COPY --from=build /app/target/*.jar app.jar
# Expone el puerto (informativo)
EXPOSE 8080
# Comando para arrancar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]