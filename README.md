docker-flask-sockets
====================

Docker trusted build test.
Contains hello.py from https://github.com/kennethreitz/flask-sockets/ (overridable).

Run container
-------------

Basic :

```bash
$ sudo docker run -t -i -p 8000:8000 fspot/flask-sockets
```

Override the code inside the container and use a volume from the host (persistant) :

```
$ sudo docker run -t -i -p 8000:8000 -v /tmp/code:/code/work fspot/flask-sockets
```

Now you're in the container (bash prompt).

Launch project
--------------

Inside the container :

```bash
$ gunicorn -k flask_sockets.worker -b 0.0.0.0:8000 hello:app  # needs hello.py with app (wsgi compliant)
```

As we've bound port 8000 of the host to 8000 of the container, then :

```bash
$ curl localhost:8000
```

should work in both.

Also, open your browser and go to http://www.websocket.org/echo.html. Put `ws://localhost:8000/echo`, then connect : websocket works.

