FROM maven:3.2.3-jdk-8 as builder

WORKDIR /app

COPY sources.list /etc/apt/sources.list
COPY settings.xml /usr/share/maven/ref/
COPY pom.xml ./
COPY . .
RUN mvn clean install -DskipTests -Dmaven.test.skip=true

FROM openjdk:8-jre-alpine

WORKDIR /app

COPY --from=builder /app/target/jshERP.jar /app/app.jar

ENV JAVA_OPTS="-Djava.awt.headless=true"

EXPOSE 9999

CMD ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]