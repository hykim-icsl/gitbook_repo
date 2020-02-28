# 1. Anaconda installation & settings

## 1.1 [https://www.anaconda.com/distribution/](https://www.anaconda.com/distribution/) 사이트를 통해서 최신버전 bash 스크립트를     복사해 놓는다.

## 1.2 curl을 이용하여 Anaconda web site에서 복사한 링크를 통해 다운로드한다.

```bash
$cd /tmp    
$curl -O https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh
```

## 1.3 SHA-256 체크성을 통한 암호화 해시 확인으로 설치 프로그램의 무결성을 확인

```bash
$ sha256sum Anaconda3-2019.03-Linux-x86_64.sh
```

## 1.4 아나콘다 스크립트 실행 \(마지막에 yes 입력\)

```bash
$bash Anaconda3-2019.03-Linux-x86_64.sh
```

## 1.5 설치를 활성화한다.

```bash
$reboot
$source ~/.bashrc
```

## 1.6 아나콘다 버전 확인 후 업데이트까지 진행을 해준다.

```bash
$conda -V
$conda update conda
```

## 1.7 아나콘다 버전 체크 및 패키지 리스트 체크

아래 명령어를 통해 아나콘다 버전체크, 패키지 리스트 체크 등을 하도록 한다.  
Jupyter Notebook에서 가상환경내에서 사용가능하도록 추가적인 패키지도 설치한다.

```bash
$conda --version    #conda version check
$conda update conda #conda update
$conda list         #conda library
$conda env list     #env list
$conda install nb_conda #나중에 Jupyter Notebook에서 새로 만든 환경들이 보이게 하기 위해 필요한 작업
```

    Python3.7 & Tensorflow1.14-gpu version 환경설치

```bash
(base)$conda create --name py37tf114 python=3.7 #python 3.7version env 생성
(base)$conda env list                           #py37tf114 env 확인
(base)$conda activate py37tf114                 #py37tf114 Env 진입
(py37tf114)$conda install ipykernel             #나중에 Jupyter Notebook에서 새로 만든 환경들이 보이게 하기 위해 필요한 작업
(py37tf114)$pip install tensorflow-gpu==1.14.0  #TensorFlow-gpu 1.14.0 설치
(py37tf114)$pip install --upgrade keras
```

## 1.8 추가적인 python 패키지 설치

Deeplearning에 필요한 추가적인 python 패키지들을 추가적으로 설치한다.
```bash
$pip install jupyter theano keras matplotlib scikit_learn seaborn
$conda install pygpu
```

설치된 python package 확인한다.

```bash
$pip list | grep <package name>
```

<br><br>

# 2. Numpy error Issue

numpy version으로 인해서 error message가 발생하여 numpy version을 낮은 걸로 재설치 한다.

```bash
(py37tf114)pip show numpy 
(py37tf114)pip uninstall numpy         #numpy 제거
(py37tf114)pip install numpy==1.16.5   #낮은 버전으로 다시 설치
```
<br><br>

# 3. Rerference

* [https://nagy.tistory.com/26](https://nagy.tistory.com/26)
* [https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart](https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart)
* [https://deepcell.co.kr/92](https://deepcell.co.kr/92)

<br><br>