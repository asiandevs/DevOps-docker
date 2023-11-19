----------------------------------
# Managing Container Images
----------------------------------

![image](https://github.com/asiandevs/images/blob/2c86fad2b67f154455e2534a81fd79dbdaff47e6/docker_image.jpg)

1. **Login as "root" user on docker host:**

   ```bash
   ssh root@<dockerhost>
   ```

2. **Search for a suitable image by using the docker search command to find all the images that contain the term fedora.**

   ```bash
   docker search fedora
   ```

3. **Identified a suitable image, fedora and now download it using the docker pull command.**

   ```bash
   docker pull fedora
   ```

4. **List the images locally on host.**

   ```bash
   docker images
   ```

5. **Inspect the fedora image, to display detailed information.**

   ```bash
   docker inspect fedora
   ```

6. **Run a container, refer to a tagged image.**

   ```bash
   docker run --name mm_fedora -it fedora /bin/bash
   ```

7. **Installing Maria dB-server packages inside the image.**

   ```bash
   dnf install mariadb-server -y
   dnf install git -y
   ```
   Note: Fedora uses dnf as a Package Manager instead of yum.

8. **Exit from the interactive mode.**

   ```bash
   exit
   ```

9. **To list all the containers, run the below command.**

   ```bash
   docker ps -a
   ```
   Container Name: mm_fedora

10. **Create a new image from the container on which we made changes by running "docker commit" command.**

    ```bash
    docker commit -m "Added mariadb-server and git" -a "mmfedora" mm_fedora mm_fedora_image:ver1
    ```

    Here we used the `docker commit` command. We specified two flags: `-m` and `-a`.
    - `-m` flag allows us to specify a commit message, much like we would with a commit on a version control system.
    - `-a` flag allows us to specify an author for our update.

11. **Check images list.**

    ```bash
    docker images
    ```
