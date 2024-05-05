# docker-rust-builder-base
[![Build Image](https://github.com/infrastructure-blocks/docker-rust-builder-base/actions/workflows/build-image.yml/badge.svg)](https://github.com/infrastructure-blocks/docker-rust-builder-base/actions/workflows/build-image.yml)
[![Update From Template](https://github.com/infrastructure-blocks/docker-rust-builder-base/actions/workflows/update-from-template.yml/badge.svg)](https://github.com/infrastructure-blocks/docker-rust-builder-base/actions/workflows/update-from-template.yml)

This repository holds the definition for builder images of Rust projects. Docker Rust based images are meant to be
built using a multi-stage build. The first stage is the build stage, and the build stage can inherit from this
image.

This image is meant to be used in conjunction with the matching [runtime image](https://github.com/infrastructure-blocks/docker-rust-runtime-base/).

## Usage

Here is an example Dockerfile where a Rust project is built using this base image:

```Dockerfile
# Should be passed as a build argument.
ARG RUST_VERSION=1.75

# The base tag is the version of the Rust toolchain to use.
FROM public.ecr.aws/infrastructure-blocks/docker-rust-builder-base:${RUST_VERSION} as builder

# This base builder image uses alpine, so the runtime image should also use alpine.
FROM public.ecr.aws/infrastructure-blocks/docker-rust-runtime-base:${RUST_VERSION}
RUN apk update && apk add --no-cache <extra-runtime-dependencies>
COPY --from=builder /usr/local/cargo/bin/<your-rust-project> /usr/local/bin/<your-rust-project>
ENTRYPOINT ["<your-rust-project>"]
```
