
FROM maven:3.9.6-eclipse-temurin-11 AS builder

WORKDIR /build

COPY . .

RUN mvn clean package -DskipTests


FROM tomcat:9.0-jdk11

WORKDIR /usr/local/tomcat/webapps/

COPY --from=builder /build/target/verademo.war ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]
