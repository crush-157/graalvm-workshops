FROM ghcr.io/graalvm/graalvm-ce:22.3.2 AS build-jar

COPY . /build
WORKDIR /build

FROM build-jar AS build-native
RUN ./mvnw -Pnative native:compile
ENTRYPOINT [ "/build/target/verses" ]
