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
install segemehl:

```
curl www.bioinf.uni-leipzig.de/Software/segemehl/old/segemehl_0_2_0.tar.gz > segemehl_0_2_0.tar.gz
```
```
tar xzf segemehl_0_2_0.tar.gz
```
```
cd segemehl_*/segemehl/ && make && cd ../../
```

add segemehl to PATH
```
cp segemehl_0_2_0/segemehl/segemehl.x /usr/bin/segemehl.x
```
add lack to PATH
```
cp segemehl_0_2_0/segemehl/lack.x /usr/bin/lack.x

```
install deseq2 FAILED

install lsb-release (actually not needed for reademption etc. only for checking ubuntu version)
```
apt-get install -y lsb-release
```
Add R 3.6 mirror
```
echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" >> /etc/apt/sources.list
```

```
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
```
```
apt-get update

```
Install R
```
apt-get install r-base
```
For installing dese2 try:
```
somwhere do:
apt install libcurl4-openssl-dev
 1  apt-get update
    2  echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" >> /etc/apt/sources.list
    3  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
    4  apt-get install gnupg2 -y
    5  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
    6  apt-get update
    7  apt-get install -y ca-certificates
    8  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
    9  apt-get update
   10  apt-get install r-base
   11  R
   in R: if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

    BiocManager::install("DESeq2")

```
