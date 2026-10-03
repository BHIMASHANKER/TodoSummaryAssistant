FROM eclipse-temurin:17-jdk AS build

WORKDIR /app

COPY . .

RUN ./mvnw clean package -DskipTests

FROM eclipse-temurin:17-jre

WORKDIR /app

RUN useradd -r -u 1001 appuser

COPY --from=build /app/target/todo-summary-assistant-0.0.1-SNAPSHOT.jar app.jar

RUN chown appuser:appuser app.jar

USER appuser

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]