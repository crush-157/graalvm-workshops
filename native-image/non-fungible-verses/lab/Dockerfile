FROM ghcr.io/graalvm/graalvm-ce:22.3.2 AS build-jar

COPY . /build
WORKDIR /build
RUN ./mvnw clean package
ENTRYPOINT [ "java", "-jar", "./target/verses-0.0.1-SNAPSHOT.jar" ]

FROM build-jar AS build-native
RUN ./mvnw -Pnative native:compile
ENTRYPOINT [ "/build/target/verses" ]

FROM build-jar AS build-distroless
RUN ./mvnw --file distroless-pom.xml --no-transfer-progress -Pnative native:compile

FROM gcr.io/distroless/base AS distroless
COPY --from=build-distroless /build/target/verses .
ENTRYPOINT ["/verses"]