FROM rust:1.58.1-alpine3.14 AS prisma
ARG TARGETARCH
ARG PRISMA_ENGINES_VERSION=3.9.0

ENV RUSTFLAGS="-C target-feature=-crt-static"

RUN apk --no-cache add \
  build-base \
  direnv \
  git \
  musl-dev \
  openssl \
  openssl-dev \
  perl \
  protoc

RUN git clone --depth=1 --branch=${PRISMA_ENGINES_VERSION} https://github.com/prisma/prisma-engines.git /prisma

WORKDIR /prisma

RUN cargo build --release

RUN tar \
  -czf prisma-engines-${PRISMA_ENGINES_VERSION}.musl-${TARGETARCH}.tar.gz \
  -C /prisma/target/release \
  introspection-engine migration-engine prisma-fmt query-engine
