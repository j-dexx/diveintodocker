docker container run -it --name web1_3 -p 5000:5000 -e FLASK_APP=app.py -d --restart on-failure web1

--restart flag telling docker to restart on failure
-p 5000:5000 is bind hosts host_computer:docker_container
-d tells docker to run in the background
-e allows you to pass an environment variable, you can pass multiple.

docker container run -it --rm --name web1_2 -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1

--rm flag tells docker to remove container when stopped

-it flag tells docker to use interactive terminal


