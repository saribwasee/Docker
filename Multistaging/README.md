# Multi-stage

Multi-stage builds are a feature introduced in Docker 17.05. They allow developers to create a Dockerfile that defines multiple stages for building an image. Each stage can have its own set of instructions and build context, which means that the resulting image can be optimized for size and performance. In a multi-stage build, each stage produces an intermediate image that is used as the build context for the next stage. The final stage produces the image that will be used to run the application.

The key advantage of using multi-stage builds is that it allows developers to reduce the size of the final image. By breaking down the build process into smaller stages, it becomes easier to remove unnecessary files and dependencies that are not needed in the final image. This can significantly reduce the size of the image, which can lead to faster deployment times and lower storage costs.

