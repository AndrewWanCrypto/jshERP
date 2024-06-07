FROM maven:3.2.3-jdk-8 as builder

WORKDIR /app

COPY pom.xml ./
COPY . .
RUN mvn clean install

FROM openjdk:8-jre-alpine

WORKDIR /app

COPY --from=builder /app/target/jshERP.jar /app/app.jar

EXPOSE 9999

CMD ["java", "-jar", "app.jar"]