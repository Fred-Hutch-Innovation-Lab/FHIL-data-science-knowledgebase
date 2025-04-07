---
title: Containerization
parent: Reproducibility
---

# Containerization

Containers allow you to package an application with all of its dependencies into a standardized unit for software development. This is useful for developing robust workflows and publishing reproducible analyses. Docker is the most common containerization platform. Singularity (now called Apptainer) is a container platform designed for HPC environments. It is similar to Docker and can use docker images without root permissions.

## Key Concepts

- **Container**: A lightweight, standalone, executable package
- **Image**: A read-only template with instructions for creating a container
- **Dockerfile**: Instructions for building an image
- **Registry**: Storage and distribution system for images

## Best Practices

1. **Use Official Images**: Start with official base images when possible
2. **Minimize Layers**: Combine RUN commands to reduce image size
3. **Security**: Run containers as non-root users
4. **Resource Management**: Set appropriate resource limits
5. **Documentation**: Include clear instructions in Dockerfiles
6. **Version Control**: Tag images with version numbers

## Resources

- [Docker Documentation](https://docs.docker.com/)
- [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker Security Best Practices](https://docs.docker.com/engine/security/)
- [Apptainer Documentation](https://apptainer.org/docs/)
