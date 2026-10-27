# ---------- Etapa 1: build ----------
# TODO: imagen base JDK 21 de eclipse-temurin, con nombre de etapa "build"
FROM eclipse-temurin:21-jdk AS build
# TODO: carpeta de trabajo /app
WORKDIR /app
# TODO: copiar mvnw, la carpeta .mvn y pom.xml (lo que cambia poco)
COPY mvnw pom.xml ./
COPY .mvn .mvn
# TODO: descargar dependencias (dependency:go-offline)
RUN ./mvnw dependency:go-offline -B

# TODO: copiar la carpeta src
COPY src src
# TODO: empaquetar el jar sin ejecutar tests
RUN ./mvnw package -DskipTests -B

# ---------- Etapa 2: runtime ----------
FROM eclipse-temurin:21-jre
WORKDIR /app
RUN groupadd --system app && useradd --system --gid app --no-create-home app
COPY --from=build /app/target/pagos-0.0.1-SNAPSHOT.jar app.jar
USER app
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
