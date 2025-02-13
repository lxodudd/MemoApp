FROM openjdk:21-jdk-slim AS build
WORKDIR /app

COPY build.gradle settings.gradle ./
COPY gradle ./gradle
COPY gradlew ./gradlew
RUN chmod +x gradlew
RUN ./gradlew dependencies --no-daemon

COPY src ./src
RUN ./gradlew build --no-daemon -x test

FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

COPY --from=build /app/build/libs/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]