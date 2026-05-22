# --- ETAPA 1: Compilación de la aplicación con Maven ---
FROM maven:3.8.8-eclipse-temurin-17 AS build
WORKDIR /app

# Copiar el archivo de configuración de dependencias (POM) y el código fuente
COPY pom.xml .
COPY src ./src

# Compilar el proyecto saltándose las pruebas unitarias para hacerlo rápido
RUN mvn clean package -DskipTests

# --- ETAPA 2: Entorno de ejecución ligero ---
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app

# Copiar el archivo .jar compilado desde la etapa anterior
COPY --from=build /app/target/*.jar app.jar

# Exponer el puerto por defecto de Spring Boot
EXPOSE 8080

# Comando optimizado para ejecutar la API
ENTRYPOINT ["java", "-jar", "app.jar"]