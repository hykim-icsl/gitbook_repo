---
title: "how to use X2go in docker"
permalink: /x2goindocker/
layout: single
---

Assume that you have pulled a ubuntu distribution

## x2go Setup

### 1. Server installation  

Do the below process in the container

```bash
$apt update
$apt install software-properties-common
$add-apt-repository ppa:x2go/stable
$apt-get update
$apt install x2gomatebindings
```

Check service of **x2go server**  

```bash
$service --status-all | grep x2go  
```  

Start **x2go server**  

```bash
$service x2goserver start
```  

### 2. Client installation

Install x2goclient on your host

```bash  
$apt install x2goclient  
```

### 3. Creating Image from the current container

Do the below process in the container

```bash
$docker commit <container_id> <image_name>:<tag>

ex)
$docker commit c27 hykim/ubuntu:gnuradio

```

### 4. Run new container using created image

Do the below process in the container

**-v option**  is connecting directory between host and container  
**-e option** is configuring **Environment Variables** in container

```bash
$xhost local:root
$docker run -it \
> -v /tmp/.X11-unix:/tmp/.X11-unix \
> -v /dev/snd:/dev/snd \
> -e DISPLAY=unix$DISPLAY \
> hykim/ubuntu:gnuradio
```

### 5. Check GUI application by excuting the app

```bash
$gnuradio-companion
```
