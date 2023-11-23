------------------------------------------------
# Docker basics
------------------------------------------------
![image](https://github.com/asiandevs/images/blob/769909e8c7f207ae55a334322879be1e483f3200/Dockerintro.jpg)
## comparison between Virtual Machines (VMs) and Docker Containers across various features.


| Feature               | Virtual Machines (VMs)                      | Docker Containers                       |
|-----------------------|--------------------------------------------|----------------------------------------|
| **Architecture**      | Operate on hardware virtualization. Each VM has its own OS on a hypervisor. | Use containerization, sharing the host OS's kernel. Applications and dependencies are packaged into containers. |
| **Resource Overhead** | Higher resource overhead due to running a complete OS in each VM. | Lower resource overhead as containers share the host OS's kernel. |
| **Isolation**         | Strong isolation, with each VM having its own OS. | Weaker isolation compared to VMs, as containers share the host OS's kernel. |
| **Startup Time**      | Longer startup time as VMs need to boot a full OS. | Almost instant startup, as containers only need to start the application and its dependencies. |
| **Portability**       | Less portable due to encapsulating an entire OS. | Highly portable, as containers include the application and its dependencies. |
| **Resource Utilization** | May underutilize resources due to fixed resource allocation. | Can utilize resources more efficiently, dynamically scaling based on application needs. |
| **Density**           | Lower density as VMs require more resources per instance. | Higher density, allowing more containers to run on a host due to lower resource overhead. |
| **Deployment Size**   | Larger deployment size due to the inclusion of a full OS in each VM. | Smaller deployment size as containers only include necessary dependencies, reducing image size. |
| **Security**          | Higher security due to strong isolation with separate OS instances. | Security relies on the shared kernel, which may pose risks if vulnerabilities are present. Additional security measures like container orchestration tools are often used. |
| **Versioning**        | VM images encapsulate the entire OS and application stack, making versioning more complex. | Container images capture only the application and its dependencies, facilitating easier versioning and updates. |
| **Orchestration**     | Typically managed by hypervisors and virtualization management tools. | Managed by container orchestration tools like Kubernetes, Docker Swarm, or OpenShift. |
| **Scaling**           | Scaling involves provisioning new VMs, which can be slower. | Scaling is faster as new containers can be quickly spun up. Auto-scaling is more efficient. |

-----------------------------------
## Docker Components
----------------------------------

![image](https://github.com/asiandevs/images/blob/769909e8c7f207ae55a334322879be1e483f3200/Dockerintro2.jpg)

| Component          | Description                                                                      |
|--------------------|----------------------------------------------------------------------------------|
| **Docker Client**  | Primary tool for users to interact with Docker, issues commands to the Docker daemon. Can be used via the command line or graphical interfaces. |
| **Docker Daemon**  | Background process responsible for managing Docker containers on a host system. Listens for Docker API requests, executes commands, and manages Docker objects. |
| **Docker Host**    | The system (physical or virtual machine) where the Docker daemon is running. Provides the underlying infrastructure for running Docker containers. |
| **Docker Registry** | A service for storing and distributing Docker images. Docker Hub is a public registry, and organizations often set up private registries for proprietary or sensitive images. |

**Docker Server**  | (Note: This term is often used interchangeably with Docker Daemon)

-----------------------------------------------------------------
## Relation among Dockerfile, Docker image and Docker Container
-----------------------------------------------------------------

![image](https://github.com/asiandevs/images/blob/769909e8c7f207ae55a334322879be1e483f3200/Dockerintro3.jpg)

### Dockerfile

A Dockerfile is a plain text file that contains a set of instructions for building a Docker image. It specifies the base image, sets up the environment, installs dependencies, and defines how the application should be configured. Dockerfiles are used to automate the process of creating Docker images, making it reproducible and consistent across different environments. Developers create Dockerfiles to describe the steps needed to package their applications into containers.

**Example Dockerfile:**
```dockerfile
# Use an official Node.js runtime as a base image
FROM node:14

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the application code
COPY . .

# Expose a port
EXPOSE 3000

# Define the command to run the application
CMD ["npm", "start"]
```

### Docker Image

A Docker image is a lightweight, standalone, and executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, and system tools. Images are built from Dockerfiles and can be stored in a registry. Docker images are versioned and can be shared, enabling the consistent deployment of applications across different environments. Images are the building blocks for creating Docker containers.

**Example commands to build and push a Docker image:**
```bash
# Build an image from the Dockerfile in the current directory
docker build -t my-node-app .

# Tag the image for pushing to a registry
docker tag my-node-app my-registry/my-node-app:latest

# Push the image to the registry
docker push my-registry/my-node-app:latest
```

### Docker Container

A Docker container is a runnable instance of a Docker image. It encapsulates the application and its dependencies, providing isolation and portability. Containers can be started, stopped, moved, and deleted. They run in an isolated environment on the host system, sharing the host's kernel but with their isolated file systems and processes. Multiple containers can be created from the same Docker image, each running independently of the others. Containers can communicate with each other and the host system, making them a lightweight and efficient deployment unit.

**Example commands to run a Docker container:**
```bash
# Run a container from the my-node-app image
docker run -p 8080:3000 my-node-app
```

In summary:
- A **Dockerfile** is a set of instructions for building a Docker image.
- A **Docker image** is a packaged, executable software unit that includes the application and its dependencies.
- A **Docker container** is a runnable instance of a Docker image, providing a lightweight and consistent execution environment.

The relationship is as follows:

Dockerfile (Instructions) -> Docker Image:

A Dockerfile contains instructions for building a Docker image. When you build the Dockerfile, it creates a Docker image based on those instructions.
Docker Image -> Docker Container:

A Docker image serves as a template for creating Docker containers. When you run a Docker container, it is instantiated from a specific Docker image, and it represents a live, running instance of that image.
