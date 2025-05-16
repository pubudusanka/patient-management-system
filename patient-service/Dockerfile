FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /app

# Step 1: Copy pom.xml and download dependencies
COPY pom.xml .

RUN mvn dependency:go-offline -B

# Step 2: Copy the source code
COPY src ./src

# Step 3: Package the app (skip tests for now)
RUN mvn clean package -DskipTests

# Debug: show the contents of target/
RUN ls -l target

# Step 4: Use JDK image to run app
FROM openjdk:21-jdk AS runner

WORKDIR /app

# Step 5: Copy built jar
COPY --from=builder /app/target/patient-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4000

ENTRYPOINT ["java", "-jar", "app.jar"]
