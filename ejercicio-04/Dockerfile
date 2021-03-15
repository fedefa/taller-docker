FROM openjdk:8-jre-alpine
WORKDIR /app
COPY passwordapi.jar app.jar
EXPOSE 8080
CMD ["/usr/bin/java", "-jar", "app.jar"]
