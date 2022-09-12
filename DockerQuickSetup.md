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
apt update
apt install sudo 
apt install ssh -y
service ssh start
apt install vim -y
apt install bash-completion
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
service sshd restart
su username
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
ssh username@$ipaddress -X
```
## for static ip
```
#!/bin/bash
docker start container_name
docker container exec -d container_name service ssh start   # activates ssh of container with detach mode.
# if you have assigned a static ip when you used run command 
ssh username@thatStaticIp -X
```

# note: first call may not work after boot, after first attempt it will work properly



# System Info
```
watch docker system df -v
```
