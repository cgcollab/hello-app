# hello-redis

This application returns a greeting and a counter of requests (e.g. "Hello world 5!" and "Hello sunshine 3!").

- A default greeting can be defined at startup using the environment variable HELLO_MSG (default value is "world")
- The greeting can also be modified dynamically per request using the request path (e.g. curl localhost:8080/sunshine)

The counter tracks requests per greeting message (_world_, _sunshine_, etc) and is stored in Redis.

A sample response looks like this:
```
<h1>Hello sunshine 6!</h1>
```

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
