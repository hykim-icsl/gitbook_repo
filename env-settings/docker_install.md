# Docker 설치 및 옵션

## 1. Docker Installation

```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker
```

## 2. Docker Container 실행 방법

```bash
docker run [OPTIONS] IMAGE[:TAG] [COMMAND]
# ex) docker run -it ubuntu:18.04 /bin/bash
```

## 3. Docker Options

-d : background mode  
-p : connecting port between host and container  
-v : connecting directory between host and container  
-e : configure Vars in container  
--name : naming container  
--rm : deleting container when process exits  
--it : for terminal input  
--link : connecting container \[container name:nickname\]

