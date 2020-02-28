# TensorRT Docker container를 사용하는 이유

내용작성 필요
<br><br>

TensorRT docker container를 사용하기 위해서는 Docker가 설치되어 있어야 한다.  
Docker 설치는 아래 글을 참고하도록 하자.  
[Docker 설치 링크](/env-settings/docker_install.md)

# 1. Nvidia driver install

## 1.1 Graphic card information check  

아래 커맨드를 통해서 그래픽 카드에 대한 정보를 얻을 수 있다.
```bash
1. lshw -C display
2. ubuntu-drivers devices #you can check the recommended version of driver
```

## 1.2 Installation driver (package install : apt)

```bash
add-apt-repository ppa:graphics-drivers/ppa # Add repository
apt update
apt-cache search nvidia | grep nvidia-driver-<driver version> #check if there is driver version you want to install
apt install nvidia-driver-<driver version> 
reboot
```

만약 driver를 설치하고 나서 충돌이 나는 상황에는 아래 커맨드로 nvidia driver를 삭제 후 위의 과정을 통해 다시 설치하도록 한다.
```bash
apt --purge autoremove nvidia*
```

## 1.3 Drvier version check

아래 커맨드들을 통해서 Driver version 체크가 가능하다.
```bash
1. nvidia-settings
2. nvidia-smi
3. cat /proc/driver/nvidia/version
```

Ref : <https://codechacha.com/ko/install-nvidia-driver-ubuntu/>

<br><br>

# 2.Nvidia container toolkit install

Ubuntu 16.04/18.04 버전에 해당된다.  
아래 커맨드를 통해 Nvidia container toolkit을 설치하도록 한다.

```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker
```

Ref : <https://github.com/NVIDIA/nvidia-docker>

<br><br>

# 3.TensorRT Container pull & run

아래 커맨드를 통해 TensorRT Image를 pull 한 이후 container를 생성한다.  
아래 run 커맨드 옵션에 --rm 옵션은 container를 종료시 container가 사라지므로 원치 않으면 --rm 옵션을 빼고 실행한다.

```bash
$docker pull nvcr.io/nvidia/tensorrt:18.08-py<x>
$docker run --gpus all -it --rm nvcr.io/nvidia/tensorrt:18.08-py<x>
```

Ref : <https://docs.nvidia.com/deeplearning/sdk/tensorrt-container-release-notes/running.html#running>

<br><br>


# 4. 기타 내용

* docker 19.03 이후 버전에서는 nvidia-docker 명령어 사용할 필요 없이 docker 명령어로 사용하면 된다. [https://github.com/NVIDIA/nvidia-docker](https://github.com/NVIDIA/nvidia-docker)
