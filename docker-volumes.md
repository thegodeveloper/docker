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
      - db-data:/var/lib/mysql/data
  mongo-express:
    image: mongo-express
    ...
volumes:
  db-data:
    driver: local
```