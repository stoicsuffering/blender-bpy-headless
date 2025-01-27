# Setup

### Pull base image & run

````cmd
docker pull nvidia/cuda:12.4.1-devel-ubuntu22.04

docker run --platform linux/amd64 -it nvidia/cuda:12.4.1-devel-ubuntu22.04
````

### Set up container with dependencies
```cmd
apt update
apt install python3 git git-lfs
apt install build-essential git git-lfs subversion cmake libx11-dev libxxf86vm-dev libxcursor-dev libxi-dev libxrandr-dev libxinerama-dev libegl-dev
apt install libwayland-dev wayland-protocols libxkbcommon-dev libdbus-1-dev linux-libc-dev
apt install python3.11 python3-pip python3.11-dev
```

### Copy OptiX and Blender repo to container

I already had the NVIDIA Optix 7.3 SDK and the blender repo (checked out stoicsuffering/blender-bpy-headless:blender-v4.2-release) in a zip file. Copying that to the image.
````cmd
docker ps
docker cp repo-plus-optix.zip [container_id]:/opt/repo-plus-optix.zip
````

### Set up OptiX
TODO

### Build

```cmd
cd /opt/blender-src
./build_files/utils/make_update.py --use-linux-libraries --architecture amd64

make update
make headless bpy release
```
