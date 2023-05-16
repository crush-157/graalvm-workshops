FROM ghcr.io/graalvm/graalvm-ce:22.3.2 AS builder

COPY . /build
WORKDIR /build
RUN ./mvnw clean -Pnative native:compile