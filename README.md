# Docker Ubuntu Container Setup
## Option 1
```
docker run -it --name container_name ubuntu:20.04
```
## Option 2 (if you wanna assign a static ip)
```
docker network create --subnet=172.22.0.0/16 jammyJellyfishNetwork
docker run -it --name 2204 --net jammyJellyfishNetwork --ip 172.22.0.4  ubuntu:22.04  

```
```
apt update;
apt install sudo; 
apt install ssh -y;
service ssh start;
apt install vim git curl wget build-essential gnome-shell-pomodoro -y;
source ~/.bashrc;
apt install bash-completion;
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf;
~/.fzf/install;
git clone https://github.com/pyenv/pyenv.git ~/.pyenv;
cd ~/.pyenv && src/configure && make -C src;
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc;
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc;
echo 'eval "$(pyenv init -)"' >> ~/.bashrc;
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh  # rust install
source ~/.bashrc;


adduser username  # set your username
```
```
adduser username sudo # to give sudo permission
```
### Edit and uncomment line 90 and 92 of the sshd_config file as below
###   X11Forwarding yes
###   X11UseLocalhost no
```
vim /etc/ssh/sshd_config 
```
```
service sshd restart;
su username;
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
