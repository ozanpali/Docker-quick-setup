# Docker Ubuntu Container Setup
```
docker run -it --name container_name ubuntu:20.04
```
```
apt update
apt install sudo -y 
apt install ssh -y
service ssh start
adduser username  # set your username
```
```
adduser username sudo # to give sudo permission
su username
sudo apt install vim -y
```


# Quick Launch via ssh
```
docker start container_name
docker container exec -d container_name service ssh start   # activates ssh of container with detach mode.
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name | xclip 
ipaddress=`xclip -o`
ssh username@$ipaddress -X
```

# If you are one liner
- create a file without extension at ~/bin/
- paste code below
- make it executable```
chmod +x shortcutname```
- then you can type ```shortcutname``` at any directory

```
#!/bin/bash
docker start container_name
docker container exec -d container_name service ssh start   # activates ssh of container with detach mode.
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name | xclip 
ipaddress=`xclip -o`
ssh username@$ipaddress -X
```

