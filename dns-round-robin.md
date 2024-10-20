# DNS Round Robin

## Create a Network

```shell
docker network create round-robin
c03eac206311c8e49cc985cb9c04c840d65b72b0d48c535eb96d6cb1970bd07a
```

## Create an Elastic Search Server Twice

```shell
docker container run -e "discovery.type=single-node" -e "ES_JAVA_OPTS=-Xms512m -Xmx512m" -e "xpack.security.enabled=false" -d --net round-robin --net-alias search elasticsearch:8.4.3
3389a1497012222afbf20dbcf7737150f319defde9ba326579521e7a89306af0
```

```shell
docker container run -e "discovery.type=single-node" -e "ES_JAVA_OPTS=-Xms512m -Xmx512m" -e "xpack.security.enabled=false" -d --net round-robin --net-alias search elasticsearch:8.4.3
70a1381cdb41b8f881f5699f64485140a327a75c8db1f1f14a924cb0295f636d
```

## Run a Alpine container

```shell
docker container run --rm -it --net round-robin alpine
/ # 
```

### Run nslookup search in the container

```shell
/ # nslookup search
Server:         127.0.0.11
Address:        127.0.0.11:53

Non-authoritative answer:

Non-authoritative answer:
Name:   search
Address: 172.20.0.2
```

### Curl to search service

Eventually, we should get two different `cluster_uuid`:

```shell
docker container run --rm --net round-robin centos curl -s search:9200
{
  "name" : "70a1381cdb41",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "2jTAUxKHTYuEpGKl68pmpA",
  "version" : {
    "number" : "8.4.3",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "42f05b9372a9a4a470db3b52817899b99a76ee73",
    "build_date" : "2022-10-04T07:17:24.662462378Z",
    "build_snapshot" : false,
    "lucene_version" : "9.3.0",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}
```

```shell
docker container run --rm --net round-robin centos curl -s search:9200
{
  "name" : "3389a1497012",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "3S-RitdcRm2zmJ4HEx0Nvg",
  "version" : {
    "number" : "8.4.3",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "42f05b9372a9a4a470db3b52817899b99a76ee73",
    "build_date" : "2022-10-04T07:17:24.662462378Z",
    "build_snapshot" : false,
    "lucene_version" : "9.3.0",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}
```