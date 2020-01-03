FROM openjdk:8-jdk-alpine
COPY ./target/pact-provider-0.0.1-SNAPSHOT.jar /usr/src/provider/
WORKDIR /usr/src/provider
EXPOSE 8888
CMD ["java", "-jar", "pact-provider-0.0.1-SNAPSHOT.jar"]