# Traccar

## overview
| step | status |
:----:| -----
build | <span style="color:lightgreen">✔</span>
deploy | <span style="color:lightgreen">✔</span>
run | <span style="color:lightgreen">✔</span>

## building: <span style="color:lightgreen">✔</span>
the `SIMPLE`-prefix suggests, that the content of this dockerfile is a python-script
```
cd <invehicle-dir>/kuksa-appmanager
./build.sh <architecture> (arm32v6 or amd64)
...
docker save <image ID> > SIMPLE_traccar.tar
```
building may yield the following qemu-error:
`qemu: Unsupported syscall: 384` which does not prevent building.

## deploying: <span style="color:lightgreen">✔</span>
```
docker load < DOCKER_appmanager.tar
```
this returns the ``<image ID>`` of the imported docker-image
## running: <span style="color:lightgreen">✔</span>

If installed via the Appmanager or Foreverchecker, the app will run automatically. 
Else it needs to be called with :
``` 
python -u traccar-client.py
```

or 

``` 
python3 -u traccar-client.py
```
> the -u flag disables buffered input to increase performance. The `traccar-client.ini` states, where the local GPS-server is ruunning and fdrom which file to read data, if no GPS is present.

