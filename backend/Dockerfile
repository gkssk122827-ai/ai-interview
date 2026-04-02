# 1) Build stage
FROM gradle:8.10.2-jdk21 AS builder

WORKDIR /app

# Gradle 설정 파일 먼저 복사
COPY build.gradle.kts settings.gradle.kts gradlew ./
COPY gradle gradle

# 소스 복사
COPY src src

# 실행 가능한 jar 빌드
RUN chmod +x ./gradlew && ./gradlew bootJar --no-daemon

# 2) Run stage
FROM eclipse-temurin:21-jre

WORKDIR /app

# 타임존 설정(선택)
ENV TZ=Asia/Seoul

# 빌드 결과 복사
COPY --from=builder /app/build/libs/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]