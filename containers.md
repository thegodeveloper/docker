# Containers

## Create a Container

```shell
docker run --env POSTGRES_PASSWORD=passw0rd --publish 5432:5432 --name postgres-docker-course --detach postgres:15.1-alpine
...
PostgreSQL init process complete; ready for start up.

2024-10-16 14:45:42.412 UTC [1] LOG:  starting PostgreSQL 15.1 on aarch64-unknown-linux-musl, compiled by gcc (Alpine 12.2.1_git20220924-r4) 12.2.1 20220924, 64-bit
2024-10-16 14:45:42.412 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
2024-10-16 14:45:42.412 UTC [1] LOG:  listening on IPv6 address "::", port 5432
2024-10-16 14:45:42.416 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
2024-10-16 14:45:42.418 UTC [50] LOG:  database system was shut down at 2024-10-16 14:45:42 UTC
2024-10-16 14:45:42.419 UTC [1] LOG:  database system is ready to accept connections
```

- `--env`: Is to pass environment values.
- `--publish`: Is to map a port from the host to the container.
- `postgres:15.1-alpine`: Is the image name and tag.

### Connect to the database

```shell
psql --host=localhost --dbname=postgres --username=postgres
Password for user postgres:
psql (17.0, server 15.1)
Type "help" for help.

postgres=#
```

## Publish a NGINX container

```shell
docker container run --publish 8080:80 --detach nginx
0c1862d5f142cca36fa368193df572b1e14f192850895a62bac6a9b555130063
```

### Validate if the container is running

```shell
curl -s localhost:8080 | head -n 4
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
```

## Inspect Containers Using Docker Commands

- `docker container top` - Process list in one container.
- `docker container inspect` - Details of one container config.
- `docker container stats` - Performance stats for all containers.

### Docker Container Top

```shell
docker container top postgres-docker-course
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
70                  88248               88229               0                   20:08               ?                   00:00:00            postgres
70                  88313               88248               0                   20:08               ?                   00:00:00            postgres: checkpointer
70                  88314               88248               0                   20:08               ?                   00:00:00            postgres: background writer
70                  88316               88248               0                   20:08               ?                   00:00:00            postgres: walwriter
70                  88317               88248               0                   20:08               ?                   00:00:00            postgres: autovacuum launcher
70                  88318               88248               0                   20:08               ?                   00:00:00            postgres: logical replication launcher
```

### Docker Container Inspect

```shell
docker container inspect postgres-docker-course
[
    {
        "Id": "90019f444faaa4604546d379e166ffad866f8672c559038ad99110628cbdf3b8",
        "Created": "2024-10-17T20:08:12.559345006Z",
        "Path": "docker-entrypoint.sh",
        "Args": [
            "postgres"
        ],
        "State": {
...
```

### Docker Container Stats

```shell
docker container stats postgres-docker-course
CONTAINER ID   NAME                     CPU %     MEM USAGE / LIMIT    MEM %     NET I/O       BLOCK I/O     PIDS
90019f444faa   postgres-docker-course   0.00%     23.14MiB / 15.6GiB   0.14%     1.05kB / 0B   0B / 41.1MB   6
CONTAINER ID   NAME                     CPU %     MEM USAGE / LIMIT    MEM %     NET I/O       BLOCK I/O     PIDS
90019f444faa   postgres-docker-course   0.00%     23.14MiB / 15.6GiB   0.14%     1.05kB / 0B   0B / 41.1MB   6
CONTAINER ID   NAME                     CPU %     MEM USAGE / LIMIT    MEM %     NET I/O       BLOCK I/O     PIDS
90019f444faa   postgres-docker-course   0.00%     23.14MiB / 15.6GiB   0.14%     1.05kB / 0B   0B / 41.1MB   6
```

***Press CTRL+C to cancel***

## Getting shell into containers

- `docker container run -it` - Start new container interactively.
- `docker container exec -it` - Run additional command in existing container.

### Using run -it

```shell
docker container run -it --name mariadb --publish 3306:3306 mariadb sh                                                                                                      ─╯
Unable to find image 'mariadb:latest' locally
latest: Pulling from library/mariadb
1f6304731171: Already exists 
d0a18beac8bf: Pull complete 
aca8a8e17e98: Pull complete 
9ffe471e6e02: Pull complete 
53eca382844f: Pull complete 
a287069788e5: Pull complete 
2575bdc3586e: Pull complete 
6ab219cecbc8: Pull complete 
Digest: sha256:4a1de8fa2a929944373d7421105500ff6f889ce90dcb883fbb2fdb070e4d427e
Status: Downloaded newer image for mariadb:latest
# ps
  PID TTY          TIME CMD
    1 pts/0    00:00:00 sh
    7 pts/0    00:00:00 ps
#
```

***When I exit, the container stop:***

```shell
docker container ls -a                                                                                                                                                      ─╯
CONTAINER ID   IMAGE      COMMAND                  CREATED              STATUS                        PORTS     NAMES
d66cbfbd2c64   mariadb    "docker-entrypoint.s…"   About a minute ago   Exited (127) 10 seconds ago             mariadb
```

### Using exec -it

```shell
docker container run --name mariadb --publish 3306:3306 --detach -e MARIADB_ALLOW_EMPTY_ROOT_PASSWORD=yes mariadb
fd4eb83c17e056c43c83ce1aa4c8034a89e00c9fccd0dceba9578540fdf284df
```

#### Connect to an existing running container

```shell
docker container exec -it mariadb bash
root@1455a7ad31a9:/# ps -a
  PID TTY          TIME CMD
  142 pts/0    00:00:00 ps
root@1455a7ad31a9:/#
```