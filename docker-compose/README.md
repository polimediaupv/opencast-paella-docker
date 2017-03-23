# Docker compose files

These Docker compose files can be used to quickly try out the Opencast system in
different configurations. They are not designed to be production instances, but
rather quick and dirty dev/demo instances.

These Docker compose files are bassed on the official docker compose files
replacing the presentation docker image with the equivalent image with paella bundle installed.

## Images replacement

| Official image  | Replaced by (with paella bundle) |
| ------------- | ------------- |
| [opencast/allinone](https://hub.docker.com/r/opencast/allinone/)  | [polimediaupv/opencast-allinone-paella](https://hub.docker.com/r/polimediaupv/opencast-allinone-paella/)  |
| [opencast/presentation](https://hub.docker.com/r/opencast/presentation/)  | [polimediaupv/opencast-presentation-paella](https://hub.docker.com/r/polimediaupv/opencast-presentation-paella/)  |
| [opencast/adminpresentation](https://hub.docker.com/r/opencast/adminpresentation/)  | [polimediaupv/opencast-adminpresentation-paella](https://hub.docker.com/r/polimediaupv/opencast-adminpresentation-paella/)  |


## Usage

Within this directory you simply can run these commands to startup an Opencast
system:

```sh
# set an environment variable with a valid IP address to the Docker host
$ export HOSTIP=10.25.40.2
$ docker-compose -f <docker-compose-file>.yml up
```

There are multiple compose files you can choose from, showcasing the different
ways one can use the Docker images:

* [**`docker-compose.allinone.hsql.yml`**](docker-compose.allinone.hsql.yml)  
  This setup starts a simple allinone Opencast distribution with an Apache
  ActiveMQ Server and the internal HSQL Database.

* [**`docker-compose.allinone.mariadb.yml`**](docker-compose.allinone.mariadb.yml)  
  This setup starts a simple allinone Opencast distribution with an Apache
  ActiveMQ server and an external MariaDB server.

* [**`docker-compose.multiserver.mariadb.yml`**](docker-compose.multiserver.mariadb.yml)  
  This setup starts a multiserver Opencast distribution with one admin, worker
  and presentation server as well as an Apache ActiveMQ server and an external
  MariaDB server.