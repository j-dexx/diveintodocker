`docker container run -it --rm --name testingelixir elixir:1.5-alpine iex`

Will just pull down the elixir:1.5-alpine linux image from docker hub and drop
into an IEX prompt

`docker container run -it --name web1_3 -p 5000:5000 -e FLASK_APP=app.py -d --restart on-failure web1`

--restart flag telling docker to restart on failure
-p 5000:5000 is bind hosts host_computer:docker_container
-d tells docker to run in the background
-e allows you to pass an environment variable, you can pass multiple.

`docker container run -it --rm --name web1_2 -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1`

--rm flag tells docker to remove container when stopped

-it flag tells docker to use interactive terminal

`docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v $PWD:/app web1`

-v $PWD:/app tells docker to mount the current working directory to the app
folder in docker - using /app as that is the directory we use in the dockerfile.
This allows docker to do live code reloading in development but for production
we'd need to rebuild the image once done.

`docker exec -it web1 /bin/sh`

Where web1 is the container name.  This will give you a /bin/sh session inside
the container.

Can do things like `docker exec it web1 flask --version` which will output the
flask version

All files/folders will be created as root by docker by default - in mounted
volumes this will create them as root on the host system.

`docker container exec -it --user "$(id -u):$(id -g)" web1 touch hi.txt`

The --user flag expects user:group and id -u and id -g will provide this for the
current user being used
