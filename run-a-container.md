# Run a Container

## Create a Container

```shell
docker run --env POSTGRES_PASSWORD=passw0rd --publish 5432:5432 postgres:15.1-alpine
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

## Connect to the database

```shell
psql --host=localhost --dbname=postgres --username=postgres
Password for user postgres:
psql (17.0, server 15.1)
Type "help" for help.

postgres=#
```

