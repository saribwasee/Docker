# Multi-stage

### Docker Multi-Stage Build Concepts

Multi-stage builds are a feature introduced in Docker 17.05. They allow developers to create a Dockerfile that defines multiple stages for building an image. Each stage can have its own set of instructions and build context, which means that the resulting image can be optimized for size and performance. Docker multi-stage builds are a way to create more efficient and smaller Docker images by using multiple `FROM` statements in a single Dockerfile. Each `FROM` statement begins a new stage of the build. This allows you to selectively copy artifacts from one stage to another, which is particularly useful for separating the build environment from the runtime environment.

#### Key Benefits:

1. **Smaller Images**: By copying only the necessary artifacts from the build stage to the final image, you can significantly reduce the size of the final Docker image.
2. **Enhanced Security**: Exclude unnecessary tools and dependencies from the final image, reducing the attack surface.
3. **Optimized Build Process**: Different stages can use different base images tailored to the specific needs of that stage (e.g., a heavier image with build tools for building the app, and a lightweight image for running the app).

#### Example Breakdown:

Here's a detailed breakdown of the multi-stage build example:

```dockerfile
# Stage 1: Build stage
# Use a full Node.js image with all the tools needed to build the application
FROM node:21 AS builder

# Set the working directory inside the container
WORKDIR /app

# Copy the application code from the host to the container
COPY . .

# Install dependencies required for the application
RUN npm install

# Build the application (e.g., if you're using a framework like React, Vue, or Angular)
# RUN npm run build

# Stage 2: Production stage
# Use a smaller, more lightweight Node.js image for running the application
FROM node:21-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the built application from the build stage
COPY --from=builder /app .

# Expose the port the application will run on
EXPOSE 5000

# Define the command to run the application
CMD ["npm", "start"]
```

#### Detailed Steps:

1. **Build Stage**:
   - **Base Image**: `FROM node:21 AS builder` uses a Node.js image with all necessary build tools.
   - **Working Directory**: `WORKDIR /app` sets the working directory inside the container to `/app`.
   - **Copy Source Code**: `COPY . .` copies all files from the host's current directory to the container's `/app` directory.
   - **Install Dependencies**: `RUN npm install` installs all required dependencies for the application.

2. **Production Stage**:
   - **Base Image**: `FROM node:21-slim` uses a smaller Node.js image for the runtime environment.
   - **Working Directory**: `WORKDIR /app` sets the working directory inside the container to `/app`.
   - **Copy Built Application**: `COPY --from=builder /app .` copies the application from the build stage to the current stage.
   - **Expose Port**: `EXPOSE 5000` makes port 5000 available to the outside world.
   - **Start Command**: `CMD ["npm", "start"]` specifies the command to run the application.

#### Use Cases:

- **Web Applications**: Building the frontend in one stage and serving it in another.
- **Microservices**: Compiling a service with all dependencies in one stage and running it in a minimal container.
- **Continuous Integration/Continuous Deployment (CI/CD)**: Integrating multi-stage builds into pipelines for efficient and optimized container builds.

Multi-stage build an advanced feature of Docker that help optimize the building process and create more secure, smaller, and efficient Docker images.
