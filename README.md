# docker-base-image-template
[![Build Image](https://github.com/infrastructure-blocks/docker-base-image-template/actions/workflows/build-image.yml/badge.svg)](https://github.com/infrastructure-blocks/docker-base-image-template/actions/workflows/build-image.yml)
[![Trigger Update From Template](https://github.com/infrastructure-blocks/docker-base-image-template/actions/workflows/trigger-update-from-template.yml/badge.svg)](https://github.com/infrastructure-blocks/docker-base-image-template/actions/workflows/trigger-update-from-template.yml)

This template repository is for repos that hold Docker base images. Those images are made to be built programmatically
and on-demand. This is unlike application images, which should be rebuilt on every pull request.

## Instantiating the template

Upon instantiating the template repository, developers should do the following:
- Remove the [trigger update from template workflow](.github/workflows/trigger-update-from-template.yml)
- Update the README.md header and project description, in addition to this section.
- Redirect the badges to the correct repository.
- Remove/update the code owners file.
- Rename the service and the docker image in the [docker compose](./docker/docker-compose.yml) file.
- Update the [build-image](./.github/workflows/build-image.yml) workflow inputs to reflect the new image's
build requirements (for example, configure the build arguments).
