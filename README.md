# docker-rust-builder-base
[![Build Image](https://github.com/infrastructure-blocks/docker-rust-builder-base/actions/workflows/build-image.yml/badge.svg)](https://github.com/infrastructure-blocks/docker-rust-builder-base/actions/workflows/build-image.yml)
[![Update From Template](https://github.com/infrastructure-blocks/docker-rust-builder-base/actions/workflows/update-from-template.yml/badge.svg)](https://github.com/infrastructure-blocks/docker-rust-builder-base/actions/workflows/update-from-template.yml)

This repository holds the definition for builder images of Rust projects. Docker Rust based images are meant to be
built using a multi-stage build. The first stage is the build stage, and the build stage can inherit from this
image.

This image is based off of `alpine` images, so the matching runtime image should also be based off of `alpine`.

## Usage

Here is an example Dockerfile where a Rust project is built using this base image:

```Dockerfile
# The base tag is the version of the Rust toolchain to use.
FROM public.ecr.aws/infrastructure-blocks/docker-typescript-action-base:1.75 as builder

# This base builder image uses alpine, so the runtime image should also use alpine.
FROM alpine
RUN apk update && apk add --no-cache <extra-runtime-dependencies>
COPY --from=builder /builder/<your-rust-project> /usr/local/bin/<your-rust-project>
CMD ["<your-rust-project>"]
```
