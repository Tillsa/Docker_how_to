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
create a new ubuntu container:
```
$ docker create ubuntu
```
create a new ubuntu container using a tag (otherwise the latest version will be pulled):
```
$ docker create ubuntu:18.04

```
