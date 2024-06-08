FROM inrgihc/maven-aliyun:3.6.3-jdk-8 as builder

WORKDIR /app

COPY pom.xml ./
COPY . .
RUN mvn clean install -DskipTests

FROM openjdk:8u201-jre-alpine3.9

WORKDIR /app

RUN apk --no-cache add ttf-dejavu fontconfig

COPY --from=builder /app/target/jshERP.jar /app/app.jar

ENV JAVA_OPTS="-Djava.awt.headless=true"

EXPOSE 9999

CMD ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]