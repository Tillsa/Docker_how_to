# Docker Tutorial
### Install docker 
Instructions taken from https://docs.docker.com/install/linux/docker-ce/ubuntu
```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

```
$ sudo apt-get update
```
```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```
$ sudo apt-key fingerprint 0EBFCD88
    
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
```
$ sudo apt-get update
```
```
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

### Use docker without typing sudo
```
$ sudo usermod -aG docker $USER
```
log user out and in again to make the changes work

## Docker commands
remove all stopped containers, networks not used by at leeast one container, all dangling images, all danglig build cache
```
$ docker system prune
```
show all images:
```
$ docker image ls
```
remove an image:
```
$ docker image rm <IMAGE ID>
```
remove a container via iage id (e.g. 3b70ac11dc39):
```
$ docker container rm <IMAGE ID>
```
create a new ubuntu container:
```
$ docker create ubuntu
```
create a new ubuntu container using a tag (otherwise the latest version will be pulled):
```
$ docker create ubuntu:18.04

```
## Create a running Ubuntu image
```
docker run -it ubuntu:18.04 bash

```
```
docker start <IMAGE ID>

```
```
docker attach <IMAGE ID>

```

## Copy a folder or file to the container
```
docker cp READemption-0.4.3 0bb166ccdef8:/home/READemption-0.4.3
```
## Install READemption inside docker
```
apt get update
```
```
sudo apt-get install python3 python3-setuptools python3-pip python3-matplotlib cython3 zlib1g-dev  make libncurses5-dev r-base libxml2-dev
```
```
pip3 install pysam
```
```
pip3 install biopython
```
```
pip3 install pandas
```