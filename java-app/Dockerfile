# Stage 1: Build the application
FROM maven:3.8.4-openjdk-17-slim AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the Maven configuration file
COPY pom.xml .

# Download the dependencies (this will be cached unless pom.xml changes)
RUN mvn dependency:go-offline -B

# Copy the source code
COPY src ./src

# Build the application
RUN mvn package -DskipTests

# Stage 2: Create the final image
FROM openjdk:17-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the jar file from the builder stage
COPY --from=builder /app/target/demo-1.0-SNAPSHOT.jar ./app.jar

# Specify the command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]

