# docker
Learn Docker
Here’s the **complete Docker documentation for Ubuntu** in the **same format** as your example, ensuring consistency and clarity throughout:

---

```markdown
# Docker Documentation for Ubuntu 🐳

This guide provides a comprehensive overview of Docker on **Ubuntu**, including installation, core concepts, commands, Dockerfile, Docker Compose, networking, volumes, and best practices.

---

## Table of Contents
1. # installation
2. [Core Concepts](#core-concepts)
3. [Basic Commands](#basic-commands)
4. [Dockerfile](#dockerfile)
5. [Docker Compose](#docker-compose)
6. [Networking](#networking)
7. [Volumes](#volumes)
8. [Best Practices](#best-practices)
9. [Troubleshooting](#troubleshooting)
10. [Resources](#resources)

---

## **Installation**
Follow these steps to install Docker on Ubuntu.

### **Step 1: Update System**
Update your package list to ensure you have the latest versions of software:
```bash
sudo apt-get update
```

### **Step 2: Install Docker and Verify**
Run the following commands to install Docker, its dependencies, and verify the installation:
```bash
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
sudo docker --version
sudo docker run hello-world
```

---

## **Core Concepts**
- **Image**: A read-only template with instructions for creating a container.
- **Container**: A running instance of an image.
- **Dockerfile**: A text file with instructions to build an image.
- **Docker Hub**: A cloud-based registry for Docker images.
- **Volume**: Persistent storage for containers.
- **Network**: Enables communication between containers.

---

## **Basic Commands**
### **Image Management**
```bash
sudo docker pull <image-name>      # Pull an image
sudo docker images                # List images
sudo docker rmi <image-id>        # Remove an image
```

### **Container Management**
```bash
sudo docker run -d --name <container-name> <image-name>  # Run a container
sudo docker ps                                          # List running containers
sudo docker stop <container-id>                         # Stop a container
sudo docker rm <container-id>                           # Remove a container
```

### **Logs and Monitoring**
```bash
sudo docker logs <container-id>   # View logs
sudo docker stats                 # Monitor resource usage
```

---

## **Dockerfile**
A `Dockerfile` is a script to build a Docker image. Here’s an example:

```Dockerfile
# Use an official base image
FROM ubuntu:20.04

# Set environment variables
ENV APP_HOME /app

# Install dependencies
RUN apt-get update && apt-get install -y python3

# Copy application code
COPY . $APP_HOME

# Set working directory
WORKDIR $APP_HOME

# Run the application
CMD ["python3", "app.py"]
```

**Build the Image**:
```bash
sudo docker build -t my-app .
```

---

## **Docker Compose**
Docker Compose is used to manage multi-container applications. Define services in a `docker-compose.yml` file:

```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "80:80"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: example
```

**Commands**:
```bash
sudo docker-compose up    # Start services
sudo docker-compose down  # Stop services
```

---

## **Networking**
Docker provides networking for container communication.

```bash
sudo docker network create my-network                   # Create a network
sudo docker run --network my-network <image-name>       # Run a container in a network
```

---

## **Volumes**
Volumes persist data outside containers.

```bash
sudo docker volume create my-volume                     # Create a volume
sudo docker run -v my-volume:/data <image-name>         # Mount a volume
```

---

## **Best Practices**
1. **Use Multi-Stage Builds**: Reduce image size by using multi-stage builds.
   ```Dockerfile
   FROM node:14 AS build
   WORKDIR /app
   COPY . .
   RUN npm install && npm run build

   FROM nginx:alpine
   COPY --from=build /app/dist /usr/share/nginx/html
   ```

2. **Avoid Running as Root**: Use a non-root user in your Dockerfile.
   ```Dockerfile
   RUN useradd -m myuser
   USER myuser
   ```

3. **Use `.dockerignore`**: Exclude unnecessary files from the build context.
   ```plaintext
   node_modules
   .git
   ```

4. **Keep Images Small**: Remove unused dependencies and clean up caches.
   ```Dockerfile
   RUN apt-get update && apt-get install -y \
       package1 \
       package2 \
       && apt-get clean
   ```

5. **Use Official Images**: Prefer official images from Docker Hub for reliability.

---

## **Troubleshooting**
### **Common Issues**
1. **Container Not Starting**:
   - Check logs: `sudo docker logs <container-id>`
   - Debug: `sudo docker run -it <image-name> /bin/sh`

2. **Image Build Failing**:
   - Rebuild without cache: `sudo docker build --no-cache -t my-image .`

3. **Network Issues**:
   - Inspect network: `sudo docker network inspect <network-name>`

4. **Volume Permissions**:
   - Ensure correct permissions for mounted volumes.

---

## **Resources**
- [Official Docker Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Docker Networking Guide](https://docs.docker.com/network/)

---

## **Contributing**
Feel free to contribute to this guide! If you have any questions or suggestions, open an issue or submit a pull request.

---

Happy Dockering on Ubuntu! 🐳
```

---

### Key Features of This `README.md`:
1. **Consistent Format**: Follows the same structure as your example for clarity.
2. **Comprehensive Coverage**: Includes everything from installation to advanced topics.
3. **Ready-to-Use Commands**: Provides commands and examples for quick reference.
4. **Best Practices and Troubleshooting**: Offers tips and solutions for common issues.

This `README.md` is designed to be a **one-stop guide** for Docker on Ubuntu. 🚀
