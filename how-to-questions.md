> Q. How to install docker?
<details><summary>Ans.</summary>
<p>
  <a href="https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html">AWS Doc</a>

```
###########################################
# AWS EC2
###########################################
# Uninstall any older version of dockers:

$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
$ sudo yum update -y
$ sudo amazon-linux-extras install docker
$ sudo service docker start
$ sudo usermod -a -G docker ec2-user
$ docker info

###########################################
# Ubuntu 20.4
###########################################
$ sudo apt update -y
$ sudo apt install apt-transport-https \
                   ca-certificates \
                   curl \
                   gnupg-agent \
                   software-properties-common
# Add the gpg key
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
# Verify the key
$ sudo apt-key fingerprint 0EBFCD88
# add the docker repository
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
# update
$ sudo apt-get update
# Install the three docker packages
$ sudo apt install docker-ce docker-ce-cli containerd.io
# Add ubuntu user to docker group to be able to run docker
$ sudo usermod ubuntu -aG docker
```
</p>
</details>
--------

> Q. How to run a docker image?
<details><summary>Ans.</summary>
<p>  

```
$ docker run <image-name>
  
#To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```
</p>
</details>
--------

> Q. How to see running docker containers?
<details><summary>Ans.</summary>
<p>  
  
```
#https://docs.docker.com/engine/reference/commandline/container_ls/
$ docker container ls
OR
$ docker ps -a
```
</p>
</details>
--------
