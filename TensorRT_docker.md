---
title: "How to use TensorRT docker"
permalink: /TensorRT_docker/
layout: single
---

## 1.Nvidia driver install

- Graphic card information check  

```bash
$sudo lshw -C display

or  

$ubuntu-drivers devices #you can check the recommended version of driver
```

- Installation driver (package install : apt)

```bash
$sudo add-apt-repository ppa:graphics-drivers/ppa # Add repository
$sudo apt update
$apt-cache search nvidia | grep nvidia-driver-<driver version> #check if there is driver version you want to install
$sudo apt install nvidia-driver-<driver version>
$sudo reboot

<optional> #if there's any conflict of driver version
$sudo apt --purge autoremove nvidia*
#Do the above process again
```

- Drvier version check

Use any command

```bash
1. $nvidia-settings
2. $nvidia-smi
3. $cat /proc/driver/nvidia/version
```

Ref : <https://codechacha.com/ko/install-nvidia-driver-ubuntu/>

---

## 2.Nvidia container toolkit install

### Ubuntu 16.04/18.04

```bash
$distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
$curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

$sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
$sudo systemctl restart docker
```

Ref : <https://github.com/NVIDIA/nvidia-docker>

---

## 3.TensorRT Container pull & run

```bash
$docker pull nvcr.io/nvidia/tensorrt:18.08-py<x>
$docker run --gpus all -it --rm nvcr.io/nvidia/tensorrt:18.08-py<x>
```

Ref : <https://docs.nvidia.com/deeplearning/sdk/tensorrt-container-release-notes/running.html#running>

---

## 4.Check the Container

```bash
$docker run --gpus all --rm nvcr.io/nvidia/tensorrt:18.08-py<x> nvidia-smi
```
