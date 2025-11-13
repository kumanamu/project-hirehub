# ===== Build stage =====
FROM amazoncorretto:17.0.12 as build

# 🔥 캐시 깨기용 ARG
ARG CACHE_BREAK=1

WORKDIR /app
COPY . .
RUN chmod +x ./gradlew
RUN ./gradlew clean bootJar --no-daemon

# ===== Run stage =====
FROM amazoncorretto:17.0.12
WORKDIR /app
COPY --from=build /app/build/libs/*.jar /app/server.jar
EXPOSE 8080

ENV SPRING_PROFILES_ACTIVE=aws
ENV JAVA_OPTS="--add-opens java.base/java.lang=ALL-UNNAMED"

CMD ["sh", "-c", "java $JAVA_OPTS -jar /app/server.jar"]
