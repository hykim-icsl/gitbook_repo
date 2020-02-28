## 1. Tensorrt image를 Pull해서 Tensorrt docker container를 사용한다.

#### 1.1 Nvidia-container-toolkit 설치

#### 1.2 Tensorrt image pull

```bash
$docker pull nvcr.io/nvidia/tensorrt:<tensorrt_version>-<python_version>

ex) $docker pull nvcr.io/nvidia/tensorrt:19.08-py3
```


#### 1.3 Tensorrt container run

```bash
$docker run --gpus all -it --rm  nvcr.io/nvidia/tensorrt:19.08-py3 (docker 상태 확인)
```

#### 1.4 Rerference
- https://docs.nvidia.com/deeplearning/sdk/tensorrt-container-release-notes/running.html#runningc

- docker 19.03 이후 버전에서는 nvidia-docker 명령어 사용할 필요 없이 docker 명령어로 사용하면 된다.
https://github.com/NVIDIA/nvidia-docker

---

## 2. Python, Cuda, Cudnn 버전 확인
Tensorrt를 설치하게 되면 cudnn, cuda, python 등이 설치되어 있다.  
아래 명령어를 통해서 설치 버전 확인가능

```bash
$export | grep CUDA_VERSION
$export | grep CUDNN_VERSION
```

```bash
$nvcc --version     (Cuda version확인)
!! 버전확인 문서 참조
```

---

## 3. Anaconda 설치

#### 3.1. https://www.anaconda.com/distribution/ 사이트를 통해서 최신버전 bash 스크립트를 	복사해 놓는다.

#### 3.2. curl을 이용하여 Anaconda web site에서 복사한 링크를 통해 다운로드한다.

```bash
$cd /tmp	
$curl -O https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh
```
 	
#### 3.3. SHA-256 체크성을 통한 암호화 해시 확인으로 설치 프로그램의 무결성을 확인
```bash
$ sha256sum Anaconda3-2019.03-Linux-x86_64.sh
```


#### 3.4. 아나콘다 스크립트 실행 (마지막에 yes 입력)
```bash
$bash Anaconda3-2019.03-Linux-x86_64.sh
```

#### 3.5. 설치를 활성화한다.
```bash
$reboot
$source ~/.bashrc
```

#### 3.6. 아나콘다 버전 확인 후 업데이트까지 진행을 해준다.
```bash
$conda -V
$conda update conda
```

#### 3.7 아나콘다 명령어 
```bash
$conda --version    #conda version check
$conda update conda #conda update
$conda list         #conda library
$conda env list     #env list
$conda install nb_conda #나중에 Jupyter Notebook에서 새로 만든 환경들이 보이게 하기 위해 필요한 작업
```
#### 3.8 Python3.7 & Tensorflow1.14-gpu version 환경설치
```bash
(base)$conda create --name py37tf114 python=3.7 #python 3.7version env 생성
(base)$conda env list                           #py37tf114 env 확인
(base)$conda activate py37tf114                 #py37tf114 Env 진입
(py37tf114)$conda install ipykernel             #나중에 Jupyter Notebook에서 새로 만든 환경들이 보이게 하기 위해 필요한 작업
(py37tf114)$pip install tensorflow-gpu==1.14.0  #TensorFlow-gpu 1.14.0 설치
(py37tf114)$pip install --upgrade keras
```

#### 3.9 추가적인 python 패키지 설치

```bash
$pip install jupyter theano keras matplotlib scikit_learn seaborn
$conda install pygpu
```

* 설치된 python package 확인
```bash
$pip list | grep <package name>
```


#### 3.10 Numpy error Issue
- numpy version으로 인해서 error message가 발생하여 numpy version을 낮은 걸로 재설치 한다.
```bash
(py37tf114)$pip show numpy 
(py37tf114)$pip uninstall numpy         #numpy 제거
(py37tf114)$pip install numpy==1.16.5   #낮은 버전으로 다시 설치
```

#### 3.x Rerference
- https://nagy.tistory.com/26
- https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart
- https://deepcell.co.kr/92

---

## 4. Docker에서 jupyter notebook에서 사용하도록 설정

docker container에 host port와 container port를 mapping해주는 과정이 필요하므로
docker를 commit하여 docker image로 저장한 후 port를 mapping한 새로운 container를 생성하도록 한다

```bash
$docker commit <container name> <사용자 id>/<image name>:<tag>
ex) $docker commit crazy_bubble sudond/tensorrt:19.08-py03
```

새로운 docker container를 열고 port를 mapping한다.
jupyter notebook은 default로 8888 포트를 사용한다.
* --gpus all : container에서 모든 gpu 자원을 사용하도록 하는 옵션.  
* -p [host port]:[container port] : host와 container의 port를 mapping 시키는 옵션
```bash
docker run --gpus all -it --name <cointainer name> -p <port>:<port> <imagename>:<tag> /bin/bash
ex) docker run --gpus all -it --name hykim_env -p 8888:8888 <imagename>:<tag> /bin/bash
```

실행중인 docker container에서 jupyter notebook을 사용할 폴더로 이동 후 아래 command로 Jupyter notebook을 실행한다.
```bash
jupyter notebook --ip 0.0.0.0 –allow-root
```
이후 local host의 web browser에서 127.0.0.1:8888 을 입력하고, password 입력창에 jupyter notebook 실행시 나타난 token 값을 복사하고 입력하여 로그인 한다.

## 5. Jupyter notebook 에 anaconda 가상환경 kernel 추가

가상환경을 kernel을 추가하기 위해서는 위에서 설치한 몇가지 패키지가 필요하다.
```bash
$conda install nb_conda
$conda install ipykernel  
```

Jupyter notebook에 가상환경 kernel을 추가하도록 한다.
```bash
python -m ipykernel install --user --name [virtualEnv] --display-name "[displayKenrelName]"
```

이후 실행된 jupyter notebook에서 Kernel 탭에서 change kernel을 통해 새로 추가된 kernel로 변경이 가능하다.

#### Reference
- https://data-newbie.tistory.com/113

## 6. radioML data set 

Modulation classification을 하기 위한 dataset을 구하는 방법
1. [RadioML 홈페이지](https://www.deepsig.io/datasets)에서 data set을 다운받아서 사용
2. radioML git 페이지에서 dataset generation code을 통해 data set을 생성해서 사용

아래 내용은 generation code를 사용해 data set을 생성해서 사용하는 방법을 기술한다.

#### 6.1 radioML/dataset repository를 clone하고, data set을 생성할 수 있도록 gnuradio와 몇가지 패키지를 설치한다.
```bash
git clone https://github.com/radioML/dataset.git
apt-get install gnuradio
apt-get install doxygen #gr-mapper를 설치할 때 필요하니 미리 설치해둔다
apt-get install swig
```
#### 6.2 generate_RML2016.04c.py으로 dataset을 생성하기 이전에 준비과정
generate_RML2016.04c.py 은 내부에서 gnuradio module을 사용하는데, 추가적으로 gr-mapper, gr-mediatools module이 있어야 실행가능하다.

1. gr-mapper module을 설치 (현재 폴더 하나 상위폴더에서 진행)
```bash
git clone https://github.com/gr-vt/gr-mapper.git
cd gr-mapper
mkdir build && cd build
cmake .. #could not find pkgconfig 에러가 발생하지만 이 에러는 apt-get install pkg-config로 해결
make
make install
ldconfig
```

2. gr-mediatools module을 설치 (현재 폴더 하나 상위폴더에서 진행)
```bash
git clone https://github.com/osh/gr-mediatools
cd gr-mediatools && mkdir build && cd build
cmake ..
make
make install
ldconfig
```
Make 부분에서 에러가 많이 발생하기 때문에 다음과 같이 해결한다
mediatools_audiosource_impl.cc  파일에서 다음과 같이 변경한다
d_frame = avcodec_alloc_frame(); -> d_frame = av_frame_alloc();

그리고 나서 다음을 설치해준다

```bash
apt-get install libavcodec-dev libavformat-dev libavutil-dev
make
make install
ldconfig
```
- 하지만 mediatools에 여전히 문제가 있는 것으로 보임

3. source_material 저장

```bash
git clone https://github.com/radioML/source_material.git
```
dataset/source_alphabet.py 파일을 열어서 파일의 경로를 설정해준다

예시)self.src = blocks.file_source(gr.sizeof_char, "/root/workspace/source_material/gutenberg_shakespeare.txt")

이후 generate_RML2016.04c.py python파일을 실행하면 dat 파일이 생성된다.
주의할 점은 gnuradio에서 python 2를 기반으로 되어 있어 python2 generate_RML2016.04c.py해야 오류 없이 동작된다.

---

example jupyter notebook file을 개인 github에 clone 해둘 것