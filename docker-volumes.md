# Docker Volumes

- Data Persistence
  - Databases
  - Other Stateful Applications

## What is Docker Volumes

- A host has a `Host File System`.
- A container has a `Virtual File System`.
- We can plug a `Host File System` into the container using a `Virtual File System`.
- Folder in physical host file system is mounted into the virtual file system of Docker.

## Docker Volumes Types

### Host Volumes

- Using `docker run -v /home/mount/data:/var/lib/mysql/data`.

### Anonymous Volumes

- Using `docker run -v /var/lib/mysql/data`.
- The destination volume is automatically created by Docker. `/var/lib/docker/volumes/random-hash/_data`.

### Named Volumes

- Using `docker run -v name:/var/lib/mysql/data`.
- The name definition is made in Docker and is referencing a Host File System.

## Docker Compose

### Named Volumes

`mongo-docker-compose.yaml` definition:

```yaml
version: '3'
services:
  mongodb:
    image: mongo
    ports:
      - 27017:27017
    volumes:
      - db-data:/var/lib/mongo/data
  mongo-express:
    image: mongo-express
    ports:
      - 27018:27018
    volumes:
      - db-data:/var/lib/mongo-express/data
volumes:
  db-data:
    driver: local
```

## Docker Volumes Locations

In the main operating systems the Docker volumes are located in the following directories:

- Windows: `C:/ProgramData/docker/volumes`.
- Linux: `/var/lib/docker/volumes`.
- macOS: `/var/lib/docker/volumes`.

Each volume has its own hash id:

- `cfccfazp..xwzpoi/_data`.

**Docker for Mac** creates a `Linux Virtual Machine` and stores all the Docker data here.

## Get into the macOS Linux Virtual Machine created by Docker

### Use the Built-in SSH Command

```shell
docker run -it --rm --privileged --pid=host justincormack/nsenter1

Unable to find image 'justincormack/nsenter1:latest' locally
latest: Pulling from justincormack/nsenter1
726619a9fa8c: Pull complete
Digest: sha256:e876f694a4cb6ff9e6861197ea3680fe2e3c5ab773a1e37ca1f13171f7f5798e
Status: Downloaded newer image for justincormack/nsenter1:latest
~ # 
```
