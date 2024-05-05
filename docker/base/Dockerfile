ARG BASE

FROM rust:${BASE}-alpine
WORKDIR /builder/
ONBUILD COPY Cargo.toml Cargo.lock ./
ONBUILD COPY src ./src
ONBUILD RUN cargo install --path .
