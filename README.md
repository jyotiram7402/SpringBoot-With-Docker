# SpringBoot-With-Docker
This topic covers best practices, tutorials, and examples for packaging Spring Boot applications into Docker containers, enabling easy deployment and scalability. You'll learn how to create Dockerfiles tailored for Spring Boot, manage dependencies, optimize container images, and orchestrate multi-container applications using Docker Compose


# Spring Boot with Docker using IntelliJ IDEA and Maven

This repository demonstrates how to containerize a Spring Boot application using Docker, with Maven as the build tool, and IntelliJ IDEA as the IDE. You will learn how to pull and run the JDK, create Docker images, change ports, and run the Spring Boot application within a Docker container.

## Prerequisites

- **IntelliJ IDEA** installed.
- **Maven** installed.
- **Docker** installed.
- **Java Development Kit (JDK 17)** installed.

## Setup and Run

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/springboot-docker-example.git
cd springboot-docker-example
```

### 2. Open the Project in IntelliJ IDEA

1. Open IntelliJ IDEA.
2. Select `File -> Open` and navigate to the cloned repository.
3. Wait for IntelliJ to import the Maven project.

### 3. Pull JDK Docker Image

To ensure the correct Java version is used, you can pull the JDK 17 Docker image:

```bash
docker pull openjdk:17-jdk
```

### 4. Build the Spring Boot Application with Maven

Navigate to the project directory and build the application using Maven:

```bash
mvn clean package
```

This will generate a `JAR` file in the `target` directory.

### 5. Create a Dockerfile

Create a `Dockerfile` in the root directory of your project:

```Dockerfile
# Use the official OpenJDK 17 base image
FROM openjdk:17-jdk

# Set the working directory inside the container
WORKDIR /app

# Copy the packaged JAR file into the container
COPY target/your-app-name.jar /app/your-app-name.jar

# Specify the command to run the JAR file
ENTRYPOINT ["java", "-jar", "/app/your-app-name.jar"]

# Expose port 8080 (or the port your Spring Boot app runs on)
EXPOSE 8080
```

### 6. Build the Docker Image

Run the following command to build a Docker image from your Dockerfile:

```bash
docker build -t yourusername/springboot-docker-example .
```

### 7. Run the Docker Container

Run the Docker container using the image you just created:

```bash
docker run -p 8080:8080 yourusername/springboot-docker-example
```

This command maps port 8080 of the container to port 8080 on your local machine.

### 8. Change the Default Port

If you want to change the port on which the Spring Boot application runs:

1. Open the `application.properties` or `application.yml` file in `src/main/resources`.
2. Add the following line to change the port (e.g., to 9090):

   ```properties
   server.port=9090
   ```

3. Rebuild the application:

   ```bash
   mvn clean package
   ```

4. Update the Dockerfile to expose the new port:

   ```Dockerfile
   EXPOSE 9090
   ```

5. Rebuild the Docker image:

   ```bash
   docker build -t yourusername/springboot-docker-example .
   ```

6. Run the Docker container with the new port:

   ```bash
   docker run -p 9090:9090 yourusername/springboot-docker-example
   ```

### 9. Access the Application

Open your browser and navigate to `http://localhost:8080` (or `http://localhost:9090` if you changed the port).

### 10. Stop the Docker Container

To stop the running Docker container, find the container ID using:

```bash
docker ps
```

Then stop it using:

```bash
docker stop <container_id>
```

## Conclusion

You have successfully containerized a Spring Boot application using Docker, Maven, and IntelliJ IDEA. You also learned how to change the application port and manage Docker containers.
