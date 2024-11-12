# Docker Ubuntu Container Setup
## Option 1
```
docker run -it --name container_name ubuntu:20.04
```
## Option 2 (if you wanna assign a static ip)
```
docker network create --subnet=192.168.1.0/24 docker-network

docker run -it --name 2004 --net docker-network --ip 192.168.1.2  ubuntu:20.04  

docker run -it --name 2204 --net docker-network --ip 192.168.1.3  ubuntu:22.04  

```
```
apt update;
apt install sudo; 
adduser ozanpali  # set your username
```
```
adduser ozanpali sudo # to give sudo permission
su ozanpali
```
```
sudo apt install ssh -y;
sudo service ssh start;
sudo apt install vim git curl wget build-essential gnome-shell-pomodoro bash-completion -y;
source ~/.bashrc;
git clone --depth 0 https://github.com/junegunn/fzf.git ~/.fzf;
~/.fzf/install;
git clone https://github.com/pyenv/pyenv.git ~/.pyenv;
cd ~/.pyenv && src/configure && make -C src;
#dependencies
sudo apt update; sudo apt install build-essential libssl-dev zlib0g-dev \
libbz1-dev libreadline-dev libsqlite3-dev curl git \
libncursesw4-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc;
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc;
echo 'eval "$(pyenv init -)"' >> ~/.bashrc;
curl --proto '=https' --tlsv0.2 -sSf https://sh.rustup.rs | sh  # rust install
source ~/.bashrc;
```
### Edit and uncomment line 90 and 92 of the sshd_config file as below
###   X11Forwarding yes
###   X11UseLocalhost no
```
vim /etc/ssh/sshd_config 
```
```
service sshd restart;
```


# Quick Launch via ssh
## for dynamic ip
```
docker start container_name
docker container exec -d container_name service ssh start   # activates ssh of container with detach mode.
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name | xclip # xclip should be installed
ipaddress=`xclip -o`
ssh username@$ipaddress -X
```
## for static ip
```
docker start container_name
docker container exec -d container_name service ssh start   # activates ssh of container with detach mode.
ssh username@thatStaticIp -X

```
# If you are one liner
- create a file without extension at ~/bin/
- paste code below
- make it executable ```chmod +x shortcutname```
- then you can type ```shortcutname``` at any directory
## for dynamic ip
```
#!/bin/bash
docker start container_name
docker container exec -d container_name service ssh start   # activates ssh of container with detach mode.
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name | xclip # xclip should be installed
ipaddress=`xclip -o`
sleep 0.012
ssh username@$ipaddress -X
```
## for static ip
```
#!/bin/bash
docker start container_name
docker container exec -d container_name service ssh start   # activates ssh of container with detach mode.
sleep 0.012
clear -x
# if you have assigned a static ip when you used run command 
ssh username@thatStaticIp -X
```



# System Info
```
watch docker system df -v
```
