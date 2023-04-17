# hello-redis

This application returns a greeting and a counter of requests for that greeting.
- The default greeting is world and can be changed at startup using the environment variable HELLO_MSG 
- The greeting can also be modified dynamically per request using the request path (e.g. curl localhost:8080/sunshine)

Example requests/responses may look like this:
```
$ http -b :8080
<h1>Hello world 5!</h1>

$ http -b :8080/sunshine
<h1>Hello sunshine 6!</h1>
```

The counter is stored in Redis using the greeting message as the key (_world=5_, _sunshine=6_, etc).

## Run locally

#### Start redis
```shell
docker run -d --rm --name hello-redis -p 6379:6379 redis
```

#### Start app
```shell
go run hello-app.go
```
or:
```shell
HELLO_MSG=friend go run hello-app.go
```

#### Send requests
Use a browser or separate terminal window:
```shell
curl localhost:8080            # returns world (or value of HELLO_MSG) and counter
curl localhost:8080/sunshine   # returns sunshine and counter
```

#### Stop
Stop app with `<Ctrl+C>`

Stop redis with:
```shell
docker stop hello-redis
```
