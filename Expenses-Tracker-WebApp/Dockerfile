FROM maven:3.8.3-openjdk-17 AS builder

WORKDIR /app

COPY . .

RUN mvn clean install -DskipTests=true

FROM openjdk:17-alpine

WORKDIR /app

# Make sure the file name matches what you run
COPY --from=builder /app/target/*.jar /app/expensesapp.jar

CMD ["java", "-jar", "expensesapp.jar"]

