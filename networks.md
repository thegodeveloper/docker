# Docker Networks

## Concepts

- Each container connected to a private virtual network "bridge".
- Each virtual network routes through NAT firewall on host IP.
- All containers on a virtual network can talk to each other without `-p`.
- Best practice is to create a new virtual network for each app.
- Batteries included, but removable.
- Defaults work well in many cases, but easy to swap out parts to customize it.
- Make new virtual networks.
- Attach containers to more than one virtual network (or none).
- Skip virtual networks and use host IP (--net=host).
- Use different Docker network drivers to gain new abilities.

## Deploy a Container

```shell
docker container run -p 8080:80 --name webhost -d nginx
838dc5efd1ecd4004ff3aceb67aa4bde103fea2fec6d0b01d8c42e8cfc47c638
```

### Check the Ports Used by the Container

```shell
docker container port webhost
80/tcp -> 0.0.0.0:8080
```

### Get the Network IP Address

```shell
docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost
172.17.0.2
```

### List the Docker Networks

```shell
docker network list
NETWORK ID     NAME      DRIVER    SCOPE
021ce3782cd2   bridge    bridge    local
26684941d39b   host      host      local
7ffffdf3f8e3   kind      bridge    local
66bb474ffccb   none      null      local
```

## Docker Networks: CLI Management

- Show networks `docker network list`.
- Inspect a network `docker network inspect`.
- Create a network `docker network create --driver`.
- Attach a network to a container `docker network connect`.
- Detach a network from container `docker network disconnect`.

## Network none

- Removes `eth0` and only leaves you with localhost interface in container.

## Create a network

```shell
docker network create learning_docker
020079426e7b2f1e0f0793d83188c21f3beaf5ead7f138b2fc5c75a88a4553d6
```

### List the networks

```shell
docker network list
NETWORK ID     NAME              DRIVER    SCOPE
021ce3782cd2   bridge            bridge    local
26684941d39b   host              host      local
7ffffdf3f8e3   kind              bridge    local
020079426e7b   learning_docker   bridge    local
66bb474ffccb   none              null      local
```

### Create a container in the Network

```shell
docker container run --detach --name new_nginx --network learning_docker --publish 9090:80 nginx:alpine
a1466fbf506858dcc5e4f4a7f3dd80c928a9ae66154290c655c8c0fa6ea2f607
```

### Inspect the network

```shell
docker network inspect learning_docker
```

### Connect a container to a network

```shell
docker network connect 020079426e7b bca4f4cbfc
```

### Inspect the Docker Container

```shell
docker container inspect webhost
            "Networks": {
                "bridge": {
                "learning_docker": {          
```

### Disconnect a container from a network

```shell
docker network disconnect 020079426e7b bca4f4cbfc
```

### Inspect the Docker Container

Now the container shouldn't be part to the `learning_docker` network.

```shell
docker container inspect webhost
            "Networks": {
                "bridge": {
```

## Default Security

- Create your apps so frontend/backend sit on same Docker network.
- Their inter-communication never leaves the host.
- All externally exposed ports closed by default.
- You must manually expose via `-p`, which is better default security.
- This gets even better later with Swarm and Overlay networks.