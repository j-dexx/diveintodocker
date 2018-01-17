Docker creates a network by default - bridge

Can view with `docker network ls`

By default docker will add containers to the bridge network.

Can inspect network with `docker network inspect bridge` bridge being the
network name.

`docker network create --driver bridge firstnetwork` - create a network named
firstnetwork

`docker container stop name` - Stop a container by name

`docker container run --rm -itd -p 5000:5000 -e FLASK_APP=app.py -e
FLASK_DEBUG=1 --name web2 -v $PWD:/app --net firstnetwork web2`

The --net flag allows you to specify a network.  Containers on the same network
can connect to each other by name

e.g. `docker exec web2 ping redis`

If check app.py the app uses redis as a hostname to connect to the redis
container, this works because both containers are running on the same network -
we start both on the network called firstnetwork

`docker container run --rm -itd -p 6379:6379 --name redis --net firstnetwork redis:3.2-alpine`

The bridge driver can only connect containers on one host, if you wish to
connect containers on multiple hosts you'd need to use the overlay driver


`docker volume create web2_redis` creates a named volume called web2_redis.

`docker volume ls`

`docker volume inspect web2_redis` inspect the named volume - the mountpoint
output is where the data is saved on the host

`docker container run --rm -itd -p 6379:6379 --name redis --net firstnetwork -v web2_redis:/data redis:3.2-alpine`
Using the named volume; /data because that is where the redis docker directory
expects the data to be located for restoring on reinitialising a container.

[Docker Hub](https://hub.docker.com/_/redis/)
> If persistence is enabled, data is stored in the VOLUME /data, which can be used with --volumes-from some-volume-container or -v /docker/host/dir:/data

Save the data in redis
`docker exec redis redis-cli SAVE`

