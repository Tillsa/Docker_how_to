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

## Copy a folder or file to the container (example, do not use)
```
docker cp READemption-0.4.3 0bb166ccdef8:/home/READemption-0.4.3
```


## Install Python, R and other packages needed (inside the container)
```
  $ apt-get update
  $ apt-get install python3 python3-setuptools python3-pip python3-matplotlib cython3 zlib1g-dev  make libncurses5-dev libxml2-dev
  answer yes
  echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" >> /etc/apt/sources.list
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
  apt-get update
  apt install libcurl4-openssl-dev
  apt-get install r-base
  open R
  if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
    
  BiocManager::install("DESeq2")
```
### install segemehl:
install curl
```
apt install curl
```
go to home directory
```
cd home
```
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
## Copy Reademption folder to the container (from outside the container)
```
docker cp READemption-0.4.3 32ced4ad6722:/home/READemption-0.4.3
```
## Install Python libs inside container
```
pip3 install pysam
```
```
pip3 install biopython
```
```
pip3 install pandas
```
## add READemption to PATH inside container
```
echo "PATH=$PATH:/home/READemption-0.4.3/bin" >> /root/.bashrc
```

# Install Singularity and dependencies:
## Install GO
```
$ export VERSION=1.13 OS=linux ARCH=amd64
```
```
$ wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz
```
```
$ sudo tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz
```
```
$ rm go$VERSION.$OS-$ARCH.tar.gz
```
add to Path, add following line to bashrc or zshrc:
```
$ export PATH=/usr/local/go/bin:$PATH
```
## Install Singularity
```
$ wget https://github.com/sylabs/singularity/releases/download/v3.5.2/singularity-3.5.2.tar.gz
```
```
$ tar -xzvf singularity-3.5.2.tar.gz
```
```
$ cd singularity
$ ./mconfig
```
```
$ make -C builddir
```
```
$ sudo make -C builddir install
```
# Make image from container
```
docker commit <CONTAINER ID>
```

# Push image to Docker Hub
login to docker
```
$ docker login -u tillsauerwein
```
tag image
```
$ docker tag a662564f46d5 tillsauerwein/reademption:firsttry
```
push image with tag
```
docker push tillsauerwein/reademption:firsttry
```
# Download image from docker hub and make singularity image

```
singularity build \
                reademption.img \
                docker://tillsauerwein/reademption:firsttry

```
```
singularity exec -B ${STORAGE_PATH} annogesic.img \
                annogesic --version

```
Reademption set beta prior True in Code!
