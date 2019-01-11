---
title: How-To | Install Theano with Cuda-Support in Anaconda (Arch-Linux)
date: 2017-11-08 09:47:27
tags:
  - Installation
  - Linux
  - Python
categories:
  - How-To
---
## Install Anaconda
```bash
pacman -S anaconda
```

## Ignore Anaconda-Upgrades (otherwise it will overwrite all changes)
```bash
pacman -Syu --ignore anaconda
yaourt -Syu --aur --ignore anaconda
```

## Create new Python 3.5 Environment
```bash
sudo conda create -n py35 python=3.5 anaconda
```

## Change permissions of anaconda (so that you can install without root)
```bash
sudo chown -R [User] /opt/anaconda
```

## Install Theano
```bash
source activate py35
conda install theano
```

## Install CUDA (Make sure /tmp is large enough)
```bash
yaourt -Syu --aur cuda-8.0
```

## Install cuDnn
+ Download
[cuDnn 5.1 for Cuda 8.0](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v5.1/prod_20161129/8.0/cudnn-8.0-linux-x64-v5.1-tgz)

+ Install
```bash
tar -xvzf cudnn-8.0-linux-x64-v5.1.tgz
mv ./cuda/include/* /opt/cuda/include
mv ./cuda/lib64/* /opt/cuda/lib64
```

## Create .theanorc (in ~/.theanorc)
```config
[global]
device=cuda
floatX=float32
cuda.root=/opt/cuda
## Set explicitly compiler in case gcc >= 6 is system default
gcc.cxxflags=-Wnarrowing
cxx=/usr/bin/g++-5
```

## Install Jupyter Extensions
```bash
conda install -c conda-forge jupyter_contrib_nbextensions
jupyter contrib nbextension install --user

/opt/anaconda/bin/jupyter notebook
```
