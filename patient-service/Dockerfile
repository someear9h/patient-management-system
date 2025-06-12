FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /app

COPY pom.xml .

RUN mvn dependency:go-offline -B

COPY src ./src

RUN mvn clean package

# ----------------- Runner Stage ------------------

FROM openjdk:21-jdk AS runner

WORKDIR /app

# Set heap memory limits
ENV JAVA_OPTS="-Xms512m -Xmx1024m"

COPY --from=builder /app/target/patient-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4000

ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
