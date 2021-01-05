> Q. How to install docker?
<details><summary>Ans.</summary>
<p>
  <a href="https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html">AWS Doc</a>
```
  
# AWS EC2
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

# Ubuntu 20.4
#
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
