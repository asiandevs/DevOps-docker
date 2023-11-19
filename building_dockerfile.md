## Lab 5 – Building a DockerFile

**Building Image from a Dockerfile:**

Dockerfile is used for automation of work by specifying all steps that we want on the Docker image. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using Docker build, users can create an automated build that executes several command-line instructions in succession.

1. Login as "root" user on the Docker host:

   ```bash
   ssh root@dockerhost
   ```

2. Create a directory and a Dockerfile:

   ```bash
   mkdir dummycnt
   cd dummycnt
   ```

3. Each instruction creates a new layer of the image:

   ```bash
   cat > Dockerfile <<EOF
   # This is a comment
   FROM ubuntu
   RUN apt-get update && apt-get install -y ruby ruby-dev
   EOF
   ```

   Note: The first instruction is `FROM` tells the source of our image. `RUN` instruction executes a command inside the image.

4. Now let’s take Dockerfile and use the `docker build` command to build an image:

   ```bash
   docker build -t dummycnt .
   ```

   Note: Location of Dockerfile using the `.` to indicate a Dockerfile in the current directory.

5. Add a tag to an existing image after commit or build it. We can do this using the `docker tag` command. Now, add a new tag to `dummycnt` image.

   ```bash
   docker tag dummycnt dummycnt:ver1
   ```

6. Check the image we have built on the host:

   ```bash
   docker images
   ```
