# Step 1: Build using Maven and Java 17
FROM maven:3.8.5-eclipse-temurin-17 AS build
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Step 2: Run using Java 17
FROM eclipse-temurin:17-jdk-jammy
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 10000

# Using 'sh -c' to ensure Render variables are injected
ENTRYPOINT ["sh", "-c", "java -jar app.jar --server.port=${SERVER_PORT:-10000}"]