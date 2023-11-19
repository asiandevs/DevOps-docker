
# Verify the Docker Installation

1. Run a test image in a container.
   ```
   docker run hello-world
   ```

2. The `docker ps` command only shows running containers by default. To see all containers, use the `-a` flag.
   ```
   docker ps -a
   ```

3. Take another image and run that image.
   ```
   docker run -d --name pgsql banglamon/postgres12.2
   ```

4. List all the available Docker images stored locally.
   ```
   docker images
   ```

5. To search for a Docker image, for instance, CentOS.
   ```
   docker search centos
   ```

6. Download it locally by running the following command (in this case, the CentOS image is downloaded and used).
   ```
   docker pull centos
   ```

7. List images.
   ```
   docker images
   ```

8. Run an interactive session into a container.
   ```
   docker run -dit centos
   ```
   Note: "dit" – daemon interactive terminal (to run in an active state).

9. Check all the running containers.
   ```
   docker ps -a
   ```


# Cleanup

i. To remove all the containers, run the following command:
   ```
   docker rm `docker ps -a -q` -f
   ```

ii. To remove all the images, run the following command:
   ```
   docker rmi `docker images -q` -f
   ```

iii. Verify that containers are removed:
   ```
   docker ps
   ```

iv. Verify that Docker images are removed:
   ```
   docker images
   ```
# Containers and Shells
```
docker run -it centos /bin/bash
ls
exit
```
