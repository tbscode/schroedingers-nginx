# NGINX dev proxy-pass container

Made this script for local frontend development, that has to access an API server on the web, under the same server route. But this script can be used for general development routing purposes.
This easily lets you set-up a development server with multiple proxy-pass paths to different server backend urls.

`schrodingers-nginx.sh` allows to:

- by-pass CORS and same-site policies when accessing API test server in development setting
- reroute different server API routes to one development URL
- reroute development server to host URL of backend server.


## Usage

Required:

- docker (will pull the official `nginx` docker image)
- bash

Update `SERVER_URL`, `PROXY_PATH`, `SERVER_PATH` arrays to your needs, run the script.

This will start the `nginx-proxy` docker container, default route is `localhost:3333` port can be changed via `ACESS_PORT`.

## Example

```
SERVER_URL=( "host.docker.internal:3000" "test-server.com" "test-server.com" )
PROXY_PATH=( "/" "/api2/v2/" "/web-socket" )
SERVER_PATH=( "/" "/api2/" "/socket" )
```

This routes all root traffic from `localhost:3333/` to `localhost:3000` e.g. a local development frontend. From `localhost:3333` api calls or websocket connections are passed to respective urls at `test-server.com`.

Script tested on `mac`, `linux`, `chromeos`.