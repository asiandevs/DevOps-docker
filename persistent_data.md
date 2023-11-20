# Docker Volume Management

## 1. Login as "root" user on Docker host:

```bash
ssh root@<docker>
```

## 2. Pull down the official Nginx image.

```bash
docker pull nginx
```

## 3. Create a new volume named mmvol1.

```bash
docker volume create --name mmvol1
```

## 4. List the volumes on your Docker host.

```bash
docker volume ls
```

## 5. Instantiate a Docker container with the mmvol1 volume.

```bash
docker run -it -v mmvol1:/mmvol1 --name mmlabvol nginx /bin/bash
```
```bash
root@ccc0bd4d5237:/#
```

You are now in the running container's shell prompt.

## 6. Change into the /mmvol1 directory.

```bash
cd /mmvol1
```

## 7. Create a file.

```bash
touch volfile1.txt
```

## 8. List the directory contents to make sure the file exists.

```bash
ls
```

### Come out to the container:

Note: Press `<ctrl+P+Q>` to exit the container shell. This key combination leaves the container running, returning to your Docker host’s shell.

## 9. Ensure the container is still running:

```bash
docker ps
```

Note: The STATUS should show Up instead of Exited.

###  Inspect the mmvol1 volume values.

```bash
docker volume inspect mmvol1
```

## Deleting a volume

### Stop the mmlabvol container.

```bash
docker stop mmlabvol
```

### Remove the container.

```bash
docker rm mmlabvol
```

### Remove the volume.

```bash
docker volume rm mmvol1
```

### Ensure the volume was removed.

```bash
docker volume ls
```
