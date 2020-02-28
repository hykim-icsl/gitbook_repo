---
title: "Anaconda Setting"
permalink: /Anaconda_setting/
layout: single
---

## Anaconda install

### ananconda install file download

```bash
$cd /tmp
$curl -O https://repo.anaconda.com/archive/Anaconda3-5.2.0-Linux-x86_64.sh
```

### verify the file integrity the sha256sum command  

```bash
$sha256sum  Anaconda3-5.2.0-Linux-x86_64.sh
```

### excute script

```bash
$sudo bash Anaconda3-5.2.0-Linux-x86_64.sh
```

### accept licence term -> 'yes'

### add PATH -> 'yes'

### terminal restart

```bash
$source ~/.bashrc
```

### PATH check

```bash
$cat ~/.bashrc
```

### anaconda version check

```bash
$conda -V
$conda update conda
$conda init

close and re-open current shell
```

## # Error issue

- If "permission denied" error occured

```bash
$sudo env "PATH=$PATH" conda update conda
```

- PackagesNotFoundError: The following packages are not available from current channels:

```bash
$conda config --append channels conda-forge
```

Ref : <https://nagy.tistory.com/26>
<https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart>

---

## Conda Env setting

Anaconda Prompt Terminal

<https://deepcell.co.kr/92>

...

additional install

pip install jupyter  
pip install matplotlib
pip install scikit_learn
conda install theano pygpu
pip install seaborn

cPickle = > import _pickle as cPickle
<https://qastack.kr/ubuntu/742782/how-to-install-cpickle-on-python-3-4>

load(open(...),encoding='latin1')