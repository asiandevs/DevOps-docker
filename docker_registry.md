# Docker Registry

The **Registry** is an open source stateless, highly scalable server-side application that stores and distributes Docker images.

**Login as "root" user on Docker host:**

```bash
ssh root@<dockerhost>
```

**Configuring local Docker registry:**

1. Install docker-distribution package:

   ```bash
   yum install docker-distribution -y
   ```

2. List docker-distribution contents: Use the `rpm` command to list the contents of the `docker-distribution` file in CentOS. There are nearly 200 files (mostly Python code in the package). This command shows only documentation and configuration:

   ```bash
   rpm -ql docker-distribution | grep -E "(/etc)|(/usr/share)|(systemd)"
   ```

3. Start the `docker-distribution` service:

   ```bash
   systemctl enable docker-distribution
   systemctl start docker-distribution
   systemctl status docker-distribution
   ```

**Pull an image from Docker Hub to your registry:**

You can pull an image from Docker Hub and push it to your registry. The following example pulls the `ubuntu:23.04` image from Docker Hub and re-tags it as `mm-ubuntu`, then pushes it to the local registry. Finally, the `ubuntu:23.04` and `mm-ubuntu` images are deleted locally, and the `mm-ubuntu` image is pulled from the local registry.

1. Pull the `ubuntu:23.04` image from Docker Hub:

   ```bash
   docker pull ubuntu:23.04
   docker images
   ```

2. Tag the image as `localhost:5000/mm-ubuntu`. This creates an additional tag for the existing image. When the first part of the tag is a hostname and port, Docker interprets this as the location of a registry when pushing.

   ```bash
   docker tag ubuntu:23.04 localhost:5000/mm-ubuntu
   docker images
   ```

3. Push the image to the local registry running at `localhost:5000`:

   ```bash
   docker push localhost:5000/mm-ubuntu
   docker images
   ```

4. Remove the locally cached `ubuntu:23.04` and `localhost:5000/mm-ubuntu` images so that you can test pulling the image from your registry. This does not remove the `localhost:5000/mm-ubuntu` image from your registry.

   ```bash
   docker image remove ubuntu:23.04
   docker images
   docker image remove localhost:5000/mm-ubuntu
   docker images
   ```

5. Pull the `localhost:5000/mm-ubuntu` image from your local registry:

   ```bash
   docker pull localhost:5000/mm-ubuntu
   docker images
   ```

**Cleanup:**

1. To remove all the images, run the below commands:

   ```bash
   docker rmi `docker images -q` -f
   ```

2. Verify that Docker images are removed:

   ```bash
   docker images
   ```
