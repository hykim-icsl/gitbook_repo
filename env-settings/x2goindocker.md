# X2go 설치

Docker 내에서 동작되는 GUI 어플리케이션을 사용하기 위해서 x2go를 사용한다.  
Docker 설치 및 ubuntu image는 이미 되어있다고 가정한다. Docker 설치는 아래 링크의 글을 참조한다.

[Docker 설치](docker_install.md)

## x2go Setup

### 1. Server installation

Do the below process in the container

```bash
apt update
apt install software-properties-common
add-apt-repository ppa:x2go/stable
apt-get update
apt install x2gomatebindings
```

Check service of **x2go server**

```bash
service --status-all | grep x2go
```

Start **x2go server**

```bash
service x2goserver start
```

### 2. Client installation

Install x2goclient on your host

```bash
apt install x2goclient
```

### 3. Creating Image from the current container

Do the below process in the container

```bash
docker commit <container_id> <image_name>:<tag>
# ex) docker commit c27 hykim/ubuntu:gnuradio
```

### 4. Run new container using created image

Do the below process in the container

**-v option** is connecting directory between host and container  
**-e option** is configuring **Environment Variables** in container

```bash
xhost local:root
docker run -it --gpus all -p 8080:8080 -v /tmp/.X11-unix:/tmp/.X11-unix -v /dev/snd:/dev/snd -e DISPLAY=unix$DISPLAY [docker image]```

### 5. Check GUI application by excuting the app

```bash
gnuradio-companion
```
