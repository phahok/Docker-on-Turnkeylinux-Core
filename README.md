# Setting Up a Docker Host Server on TurnkeyLinux Core
Installing Docker on TurnkeyLinux Core and enabling access by various Docker GUI tools

# Instructions
Download and Install Virtualbox

Download [**TurnkeyLinux Core**](https://www.turnkeylinux.org/download?file=turnkey-core-14.1-jessie-amd64.ova)

Double Click to Install TurnkeyLinux Core on Virtualbox, follow the prompts

> Enter your root password and confirm

> Enter your postgres password and confirm

> Enter your API key, set this to **SKIP**

> Enter your email address **SKIP** this, tab tab to skip

> Install security updates **SKIP** this, tab tab to skip

Once installation is complete the server should reboot. Take note of the servers IP Address.

Use Putty to log into the server via SSH and run the following commands.  

```bash
#Install docker
echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list.d/sources.list
apt-get update
apt-get install docker.io

#Allow Remote API Access for GUI tools
echo "DOCKER_OPTS='-H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock'" >> /etc/default/docker
service docker restart

#(Optional)Bring in Required images
docker pull turnkeylinux/lapp-14.1
docker pull turnkeylinux/lamp-14.1
```
Use a tool like [**Simple Docker UI**](https://chrome.google.com/webstore/detail/simple-docker-ui/jfaelnolkgonnjdlkfokjadedkacbnib?hl=en) to manage the docker host. You should be able to connect to [SERVER_IP_ADDRESS]:2375

#Usage
Here's an example of how you'd use it. 

1. Clone a docker file off Github
2. Build it 
3. and then run it in your docker host. 

In this example we're using TurnkeyLinux LAPP as a base image and then installing NodeJS on top of it.

##TurnkeyLAPP with NodeJS
```bash
# Clone Repo and build then build the container
git clone https://github.com/ano/TurnkeyLinux-LAPP-and-NodeJS.git
docker build -t "turnkeylinux/LAPP-and-NodeJS-14.1" .
```
