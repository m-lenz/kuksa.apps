# Docker
## Overview

| step | status |
:----:| -----
build | <span style="color:lightgreen">✔</span>
deploy | <span style="color:lightgreen">✔</span>
run | <span style="color:red">x</span>

## Build prerequisites

1. Enable docker experimental feature.

Create a daemon.json file in `/etc/docker/` and add 
```
{
 
  "experimental" : true

}
```
and restart docker daemon using  `systemctl restart docker`

https://github.com/docker/docker-ce/blob/master/components/cli/experimental/README.md

2. install  qemu-user-static package on the host machine

`sudo apt-get install qemu-user-static`

## Building <span style="color:lightgreen">✔</span>

Build Kuksa-compatible dockers from this app. The Dockerfile is supposed to 
be run through the magic build.sh wrapper.

To build for am64 do

`./build.sh amd64`

to build for a Pi

`/build.sh arm32v6`

If you try playing with the docker file directly, note that the build context
needs to be the toplevel of kuksa.invehicle

## Running <span style="color:red">x</span>
This app needs Hono credentials. It uses the following environment variables

| Variable      | What                               | 
| ------------- |------------------------------------| 
| HONOIP        | hostname or IP of your Hono        |
| HONOPORT      | port your Hono instance listens on |   
| HONOPW        |         password for hono          |
| HONODEVICE    | Your device in Hono                |
| TOKEN         | Auth Token for W3C-VIS Server      |
| EMAIL_SERVER  | IP of Email-Auth Server            |
| EMAIL_PORT    | Port of Email-Auth Server          |


```
docker run 
--env W3CVISSURL='172.17.0.1:8090/vss' 
--env HONOIP='11.11.11.111' 
--env HONOPORT='1883' 
--env HONODEVICE='sensor1' 
--env HONOPW='<hono-passwd>' 
--env TOKEN='<hawkbit-token>' 
--env EMAIL_SERVER= '52.178.47.67' 
--env EMAIL_PORT= '8080'
<image ID>

```

### ERROR
Docker misinterprets the environment-variables and tries to use the `EMAIL_SERVER`-Parameter as docker-imagename

>Unable to find image '52.178.47.67:latest' locally
docker: Error response from daemon: pull access denied for 52.178.47.67, repository does not exist or may require 'docker login'.


