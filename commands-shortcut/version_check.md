# 1. Version check

## Tensorflow version check

```bash
$python
> import tensorflow as tf
> tf.__version__
'0.12.1'
```

## Nvidia driver version check

```bash
1. $nvidia-settings
2. $nvidia-smi
3. $cat /proc/driver/nvidia/version
```

## Cuda version check

```bash
$nvcc --version # Driver API version CUDA toolkit installer
$nvdia-smi # Runtime API version by GPU driver
```

Ref : [https://stackoverflow.com/questions/53422407/different-cuda-versions-shown-by-nvcc-and-nvidia-smi](https://stackoverflow.com/questions/53422407/different-cuda-versions-shown-by-nvcc-and-nvidia-smi)

