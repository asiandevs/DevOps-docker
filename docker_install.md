# Install Docker

1. Install the Docker package
   ```
   yum install docker-engine -y
   ```
   Once Docker is installed, you will need to start the Docker daemon.

2. Run the following command to start the Docker daemon on boot.
   ```
   systemctl enable docker
   ```

3. Start the Docker daemon.
   ```
   systemctl start docker
   ```

4. Verify the status of Docker.
   ```
   systemctl status docker
   ```

5. Check the Docker version.
   ```
   docker --version
   ```

6. To get more information on a command:
   Information available like options and Management commands.
   ```
   docker --help
   ```

