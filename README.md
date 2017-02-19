Outside the container:
```sh
docker pull debian:stable
docker run --priviledged --rm -ti debian:stable bash
```
Inside the container:
```sh
apt-get update && apt-get install -y debootstrap xz-utils
targetdir=rootfs
distro=etch
mkdir $targetdir
debootstrap --arch=amd64 --no-check-gpg $distro $targetdir http://archive.debian.org/debian
cd $targetdir && tar cvJf /rootfs.tar.xz .
```
Outside the container:
```sh
docker cp <CONTAINER ID>:/rootfs.tar.xz rootfs.tar.xz
docker build -t etch -f Dockerfile .
docker run --rm -ti etch bash
```
