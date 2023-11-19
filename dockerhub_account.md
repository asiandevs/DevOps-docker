-----------------------------------------
# Creating Docker Hub Account
-----------------------------------------
Docker Hub is a registry service on the cloud that allows you to download Docker images that are built by other communities. You can also upload your own Docker built images to Docker hub. In this chapter, we will see how to download and use the Jenkins Docker image from Docker hub.

The official site for Docker hub is [Docker Hub](https://www.docker.com/community-edition#/add_ons).

1. Open [Docker Hub](https://hub.docker.com/) in the web browser, paste the URL, and do a simple sign-up on Docker hub.

2. Once you have signed up, verify your Email id and login to Docker Hub account.

3. **Push an image to Docker Hub**

   - Login into docker hub through CLI

     ```bash
     docker login -u your-docker-id
     ```
     Note: Replace "your-docker-id" with your login_id.

   - Save the Docker Id as a variable to refer to it in the next command:

     ```bash
     docker_id=`docker info | grep Username | cut -d " " -f 2`
     echo $docker_id
     ```

   - Tag the image:

     ```bash
     docker tag mm_fedora_image:ver1 $docker_id/mm_fedora_image:ver1
     ```

   - Push the image:

     ```bash
     docker push $docker_id/mm_fedora_image:ver1
     ```
     
     Note: Login to Docker Hub account and verify the "fedora_cutom_image:ver1" is pushed successfully.

4. **Pull an image from Docker Hub**

   - Verify the list of docker images:

     ```bash
     docker images
     ```

   - Remove a local image to pull the same image from Docker Hub:

     ```bash
     docker rmi $docker_id/mm_fedora_image:ver1
     ```

     ```bash
     docker images
     ```

   - Pull the image:

     ```bash
     docker pull $docker_id/mm_fedora_image:ver1
     ```

     ```bash
     docker images
     ```

5. **Now, log out from docker hub account:**

   ```bash
   docker logout
   ```

6. **Cleanup**

   - To remove all the containers run the below commands:

     ```bash
     docker rm `docker ps -a -q` -f
     ```

   - To remove all the images run the below commands:

     ```bash
     docker rmi `docker images -q` -f
     ```

   - Verify that containers are removed:

     ```bash
     docker ps
     ```

   - Verify that docker images are removed:

     ```bash
     docker images
     ```
