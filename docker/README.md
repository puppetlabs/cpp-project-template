# Build Containers

Docker container images for building C++ projects are hosted publicly on Google Container Registry at gcr.io/cpp-projects/cpp-ci. They can be pulled via `docker pull gcr.io/cpp-projects/cpp-ci:<tag>`.

Builds are currently done manually. Docs on how to push new builds are available from [Google](https://cloud.google.com/container-registry/docs/pushing-and-pulling). When adding a new build, include a new incremented integer tag (1, 2, ...) as well as a tag of the commit SHA of the Dockerfile used to generate the build.
