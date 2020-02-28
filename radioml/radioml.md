# RadioML 설치
<br><br>

# 1. Tensorrt image를 Pull해서 Tensorrt docker container를 사용한다.

tensorRT docker container 사용에 대해서는 아래 링크의 글을 참고하도록 한다.

[TensorRT docker container 설치](/env-settings/TensorRT_docker.md) 

<br><br>

# 2. Python, Cuda, Cudnn 버전 확인

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
<br><br>
# 3. Anaconda 설치
Anaconda 설치에 대해서는 아래 링크의 글을 참고하도록 한다.

[Anaconda 설치](/env-settings/Anaconda_setting.md) 

<br><br>

# 4. Docker에서 jupyter notebook에서 사용하도록 설정

docker container에 host port와 container port를 mapping해주는 과정이 필요하므로 docker를 commit하여 docker image로 저장한 후 port를 mapping한 새로운 container를 생성하도록 한다

```bash
$docker commit <container name> <사용자 id>/<image name>:<tag>
ex) $docker commit crazy_bubble sudond/tensorrt:19.08-py03
```

새로운 docker container를 열고 port를 mapping한다. jupyter notebook은 default로 8888 포트를 사용한다.

* --gpus all : container에서 모든 gpu 자원을 사용하도록 하는 옵션.  
* -p \[host port\]:\[container port\] : host와 container의 port를 mapping 시키는 옵션

  ```bash
  docker run --gpus all -it --name <cointainer name> -p <port>:<port> <imagename>:<tag> /bin/bash
  ex) docker run --gpus all -it --name hykim_env -p 8888:8888 <imagename>:<tag> /bin/bash
  ```

실행중인 docker container에서 jupyter notebook을 사용할 폴더로 이동 후 아래 command로 Jupyter notebook을 실행한다.

```bash
jupyter notebook --ip 0.0.0.0 –allow-root
```

이후 local host의 web browser에서 127.0.0.1:8888 을 입력하고, password 입력창에 jupyter notebook 실행시 나타난 token 값을 복사하고 입력하여 로그인 한다.

<br><br>

# 5. Jupyter notebook 에 anaconda 가상환경 kernel 추가

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

### Reference

* [https://data-newbie.tistory.com/113](https://data-newbie.tistory.com/113)

<br><br>

# 6. radioML data set

Modulation classification을 하기 위한 dataset을 구하는 방법 1. [RadioML 홈페이지](https://www.deepsig.io/datasets)에서 data set을 다운받아서 사용 2. radioML git 페이지에서 dataset generation code을 통해 data set을 생성해서 사용

아래 내용은 generation code를 사용해 data set을 생성해서 사용하는 방법을 기술한다.

## 6.1 radioML/dataset repository를 clone하고, data set을 생성할 수 있도록 gnuradio와 몇가지 패키지를 설치한다.

```bash
git clone https://github.com/radioML/dataset.git
apt-get install gnuradio
apt-get install doxygen #gr-mapper를 설치할 때 필요하니 미리 설치해둔다
apt-get install swig
```

## 6.2 generate\_RML2016.04c.py으로 dataset을 생성하기 이전에 준비과정

generate\_RML2016.04c.py 은 내부에서 gnuradio module을 사용하는데, 추가적으로 gr-mapper, gr-mediatools module이 있어야 실행가능하다.

1. gr-mapper module을 설치 \(현재 폴더 하나 상위폴더에서 진행\)

   ```bash
   git clone https://github.com/gr-vt/gr-mapper.git
   cd gr-mapper
   mkdir build && cd build
   cmake .. #could not find pkgconfig 에러가 발생하지만 이 에러는 apt-get install pkg-config로 해결
   make
   make install
   ldconfig
   ```

2. gr-mediatools module을 설치 \(현재 폴더 하나 상위폴더에서 진행\)

   ```bash
   git clone https://github.com/osh/gr-mediatools
   cd gr-mediatools && mkdir build && cd build
   cmake ..
   make
   make install
   ldconfig
   ```

   Make 부분에서 에러가 많이 발생하기 때문에 다음과 같이 해결한다 mediatools\_audiosource\_impl.cc 파일에서 다음과 같이 변경한다 d\_frame = avcodec\_alloc\_frame\(\); -&gt; d\_frame = av\_frame\_alloc\(\);

그리고 나서 다음을 설치해준다

```bash
apt-get install libavcodec-dev libavformat-dev libavutil-dev
make
make install
ldconfig
```

* 하지만 mediatools에 여전히 문제가 있는 것으로 보임
* source\_material 저장

```bash
git clone https://github.com/radioML/source_material.git
```

dataset/source\_alphabet.py 파일을 열어서 파일의 경로를 설정해준다

예시\)self.src = blocks.file\_source\(gr.sizeof\_char, "/root/workspace/source\_material/gutenberg\_shakespeare.txt"\)

이후 generate\_RML2016.04c.py python파일을 실행하면 dat 파일이 생성된다. 주의할 점은 gnuradio에서 python 2를 기반으로 되어 있어 python2 generate\_RML2016.04c.py해야 오류 없이 동작된다.

example jupyter notebook file을 개인 github에 clone 해둘 것

