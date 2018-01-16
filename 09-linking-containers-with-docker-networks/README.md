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
