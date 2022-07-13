# motion-docker
This is a fork of the repository https://github.com/Motion-Project/motion-docker for manually assembling the motion image when it is necessary

## Caveats
- If you use /dev/video, locally attached cameras or the database features of Motion, this container won't work for you at this stage.  
- This is built directly from git master, if you want something more stable grab a prebuilt release from [here](https://github.com/Motion-Project/motion/releases) and install manually.

## How to run

Prepare the configuration file and place it in the <your machine>/dockerapp/motion/config directory. Samples can be taken from this repository or from the motion repository. You can also find samples in the /usr/local/etc/motion/ directory if you do not mount the volume from your computer

Then you can use the example below

```
docker run -d --name=motion \
    -p 7999:7999 \
    -p 8081:8081 \
    -p 8082:8082 \
    -p 8083:8083 \
    -p 8084:8084 \
    -p 8085:8085 \
    -p 8087:8087 \
    -e TZ="Europe/Berlin" \
    -v <your machine>/dockerapp/motion/config:/usr/local/etc/motion \
    -v <your machine>/dockerapp/motion/storage:/var/lib/motion \
    --restart=unless-stopped \
    lionsitroen/motion:latest
```
## How to Update

```
docker stop motion
docker rm motion
docker pull lionsitroen/motion:latest
- rerun above 'run' command
```


## Things you may need to change
- name = a label for the container, should be motion or motion-project (but can be anything)
- ports = each -p line denotes 1 camera and its stream port
- TZ = the timezone the container will be running
          
## Release Notes

- 13/09/22 Bumped to Ubuntu 22.04 and Motion 4.4.0
- 13/09/22 Forked from https://github.com/Motion-Project/motion-docker.