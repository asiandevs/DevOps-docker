# Managing the Life Cycle of Container

  ![image](https://github.com/asiandevs/images/blob/8ac089bb7e937725f7b85f7a27cf916e5a9c300b/ContainerLifecyle.jpg)
1. **Login as “root” user on docker host:**
   ```bash
   ssh root@<hostIP>
   ```

2. **Create a new container.**
   Create a container to run it later on.
   Syntax:
   ```bash
   docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
   ```
   Note: Options are referring as
   - "-t" : tty
   - "-i" : interactive

   ```bash
   docker create --name centos01 -t -i centos /bin/bash
   docker ps -a
   ```

3. **Run docker container.**
   ```bash
   docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG….]
   ```
   The docker run command must specify an IMAGE to derive the container from.
   ```bash
   docker run --name centos03 -dit ubuntu
   docker ps -a
   ```

4. **Stop container**
   To stop the container and processes running inside the container by sending SIGTERM and then SIGKILL after a grace period.
   Syntax:
   ```bash
   docker stop <container-name or container-id>
   ```
   ```bash
   docker stop centos03
   docker ps -a
   ```

5. **Start container**
   ```bash
   docker start <container-name or container-id>
   ```
   ```bash
   docker start centos03
   docker ps -a
   ```

6. **Restart a running container**
   It is used to restart the container as well as processes running inside the container.
   Syntax:
   ```bash
   docker restart [OPTIONS] CONTAINER [CONTAINER...]
   ```
   ```bash
   docker restart centos03
   ```

7. **Pause container**
   Used to pause the processes running inside the container.
   Syntax:
   ```bash
   docker pause CONTAINER [CONTAINER...]
   ```
   ```bash
   docker pause centos03
   docker ps -a
   ```
   Note: A key difference between pausing and stopping containers is in the persistence of state. When a container is stopped, any resources allocated to it, such as memory, are released, while a paused container does not release its allocated resources.

8. **Unpause container**
   Unpause all processes within a container.
   Syntax:
   ```bash
   docker unpause CONTAINER [CONTAINER...]
   ```
   ```bash
   docker unpause centos03
   ```

9. **Daemonized container**
   Instead of running the docker container with an interactive shell, it is also possible to let the docker container run as a daemon, which means that the docker container would run in the background completely detached from the current shell. The following CentOS docker container will start as a daemonized container using “-d” option.
   ```bash
   docker run --name centos-box4 -d -it centos
   docker ps -a
   ```

10. **Rename the container**
    Rename an existing container to a NEW_NAME.
    Syntax:
    ```bash
    docker rename OLD_NAME NEW_NAME
    ```
    ```bash
    docker rename centos-box4 newcentos-box4
    docker ps -a
    ```

11. **Docker Images**
    This command lists the images stored in the local Docker repository.
    Syntax:
    ```bash
    docker images [OPTIONS] [REPOSITORY]
    ```
    ```bash
    docker images
    docker images centos
    ```

12. **Search the container**
    Search the Docker Hub for images.
    Syntax:
    ```bash
    docker search [OPTIONS] TERM
    ```
    ```bash
    docker search fedora
    docker search --filter=stars=3 fedora
    ```
    Note: Options are –
    - filter , -f : Filter output based on conditions provided
    - stars : (int) number of stars the image has

13. **Pull the container**
    To pull an image or a repository from a registry.
    Syntax:
    ```bash
    docker pull [-a|--all-tags][help]NAME[:TAG]|[REGISTRY_HOST[:REGISTRY_PORT]/]NAME[:TAG]
    -a, --all-tags=true|false
    ```
    ```bash
    docker pull fedora
    docker images
    ```

14. **RMI the container**
    Remove one or more images.
    Syntax:
    ```bash
    docker rmi [OPTIONS] IMAGE [IMAGE...]
    ```
    ```bash
    docker rmi fedora
    docker images
    ```

15. **Remove the container**
    Remove one or more containers.
    Syntax:
    ```bash
    docker rm [OPTIONS] CONTAINER [CONTAINER...]
    ```
    ```bash
    docker stop newcentos-box4
    docker rm newcentos-box4
    docker ps -a
    ```

    Note: To remove a container forcefully use the below command.
    ```bash
    docker rm newcentos-box4 -f
    ```

16. **Save the container**
    Save one or more images to a tar archive (streamed to STDOUT by default).
    Syntax:
    ```bash
    docker save [OPTIONS] IMAGE [IMAGE...]
    ```
    List out an image to keep a backup
    ```bash
    docker images
    ```

    Let’s save the image as a tar file
    ```bash
    docker save ubuntu > ubuntu-backup.tar
    ```

    ```bash
    ls -lh
    ```

17. **Load the container**
    Load an image from a tar archive or STDIN.
    Syntax:
    ```bash
    docker load [OPTIONS]
    ```
    Let’s load an image from a tar file.
    ```bash
    docker load --input ubuntu-backup.tar
    ```

18. **Export the container**
    Export the contents of a filesystem to a tar archive (streamed to STDOUT by default). Export the contents of a container’s filesystem using the full or shortened container ID or container name. The output is exported to STDOUT and can be redirected to a tar file.
    Syntax:
    ```bash
    docker export [OPTIONS] CONTAINER
    ```
    ```bash
    docker export centos03 >centos03-latest.tar
    ```

    ```bash
    ls -lh
    ```

19. **Import the container**
    Create an empty filesystem image and import the contents of the tarball (.tar, .tar.gz, .tgz, .bzip, .tar.xz, .txz) into it, then optionally tag it.
    Syntax:
    ```bash
    docker import URL|- [REPOSITORY[:TAG]]
    ```
    ```bash
    docker import centos03-latest.tar centos03-cenos:ver1
    ```

    ```bash
    docker images
    ```

20. **Attach the container**
    The docker attach command allows the user to attach to a running container using the container’s ID or name, either to view its ongoing output or to control it interactively.
    ```bash


    docker run -dit --name test1 centos
    ```

    ```bash
    docker attach test1
    ```

    Verify the list of files located in the environment
    ```bash
    ls
    ```

    Verify every process on the host:
    ```bash
    ps -ef
    ```

    ```bash
    exit
    ```

    Note: On doing an “exit” the “centos” container was stopped.

    ```bash
    docker ps -a
    ```

    ```bash
    docker start test1
    ```

    ```bash
    docker ps -a
    ```

    Create a new name as “test2” for the “centos” container
    ```bash
    docker run -d --name test2 centos /usr/bin/top -b
    ```

    ```bash
    docker attach test2
    ```

    Note: Press ctrl+c to interrupt.

    ```bash
    docker ps -a
    ```

    ```bash
    docker start test2
    ```

    ```bash
    docker ps -a
    ```

21. **Docker Stats**
    The docker stats command returns a live data stream for running containers. To limit data to one or more specific containers, specify a list of container names or ids separated by a space. Users can specify a stopped container, but stopped containers do not return any data.

    Note: To exit from each of the below commands press ctrl+c.
    ```bash
    docker stats
    ```

    ```bash
    docker stats -a
    ```

    ```bash
    docker stats test1
    ```

    ```bash
    docker stats test1 test2
    ```

22. **Get the Docker Information**
    Docker-info – Display system-wide information. This command displays system-wide information regarding the Docker installation. Information displayed includes the kernel version, the number of containers, and images. The number of images shown is the number of unique images. The same image tagged under different names is counted only once.
    Syntax:
    ```bash
    docker info
    ```

    ```bash
    docker -D info
    ```

    The global -D option tells all docker commands to output debug information.

23. **Events the container**
    Get real-time events from the server. Get event information from the Docker daemon. Information can include historical information and real-time information. Docker containers will report the following events: attach, commit, create, destroy, detach, die, exec_create, exec_detach, exec_start, export, kill, oom, pause, rename, resize, restart, start, stop, top, unpause, update.
    Syntax:
    ```bash
    docker events [OPTIONS]
    ```

    Create a date variable that will output the current date.
    ```bash
    TODAY=$(date +%F)
    echo $TODAY
    ```

    Output:
    ```bash
    2018-02-27
    ```

    ```bash
    docker events --since $TODAY
    ```

    Note: Press ctrl+c to exit.

24. **Inspect the container**
    Return low-level information on a container or image. This displays all the information available in Docker for a given container or image. By default, this will render all results in a JSON array. If the container and image have the same name, this will return container JSON for unspecified type. If a format is specified, the given template will be executed for each result.
    Syntax:
    ```bash
    docker inspect [OPTIONS] CONTAINER|IMAGE [CONTAINER|IMAGE...]
    ```

    ```bash
    docker inspect --type=image centos
    ```

25. **Copy files/folders between a container and the local filesystem.**
    The docker cp utility copies the contents of SRC_PATH to the DEST_PATH. You can copy from the container’s file system to the local machine or the reverse, from the local filesystem to the container.
    Syntax:
    ```bash
    docker cp [--help] SRC_PATH CONTAINER:DEST_PATH
    ```

    ```bash
    docker cp ubuntu-backup.tar centos03:tmp
    ```

26. **Execute the container**
    Run a command in a running container. The command started using docker exec will only run while the container’s primary process (PID 1) is running and will not be restarted if the container is restarted. If the container is paused, then the docker exec command will wait until the container is unpaused, and then run.
    Syntax:
    ```bash
    docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
    ```

    ```bash
    docker exec -it centos03 ls tmp
    ```

27. **Diff the container**
    Inspect changes on a container’s filesystem. Inspect changes on a container’s filesystem. You can use the full or shortened container ID or the container name set using docker run –name option.
    Syntax:
    ```bash
    docker diff [--help] CONTAINER
    ```

    Note:
    - C -> Changed
    - A -> Added

28. **History the container**
    Show the history of when and how an image was created.
    Syntax:
    ```bash
    docker history [OPTIONS] IMAGE
    ```

    ```bash
    docker history ubuntu
    ```

29. **Kill the container**
    Kill a running container using SIGKILL or a specified signal. The main process inside each container specified will be sent SIGKILL or any signal specified with option --signal.
    Syntax:
    ```bash
    docker kill [OPTIONS] CONTAINER [CONTAINER...]
    ```

    ```bash
    docker kill centos03
    ```
