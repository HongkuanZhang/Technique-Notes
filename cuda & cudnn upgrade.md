# Cuda10.1 upgrade

1.事前準備
```
#既にドライバーがインストールされていないかチェックする
$ dpkg -l | grep nvidia 
$ dpkg -l | grep cuda
```

2.古いcudaをアンインストール
```
$ sudo apt-get --purge remove "cuda*"
$ sudo rm -rf /usr/local/cuda* 
```

3.Cuda10.1をインストール
```
# Select target platform and get the url for download (https://developer.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda-repo-ubuntu1604-10-1-local-10.1.105-418.39_1.0-1_amd64.deb)
Operating system: Linux
Architecture: x86_64
Distribution: ubuntu
Version: 16.04
Install type: dev(local)

# Downloading deb file with url above by wget and installing according to the commands below (notice: this method will update necessary Nvidia driver automatically to the "at least version" instead of latest version)
$ wget https://developer.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda-repo-ubuntu1604-10-1-local-10.1.105-418.39_1.0-1_amd64.deb
$ sudo dpkg -i cuda-repo-ubuntu1604-10-1-local-10.1.105-418.39_1.0-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install cuda

# add path in .zshrc
export PATH=/usr/local/cuda-10.1/bin:$PATH  
export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64:$LD_LIBRARY_PATH
export CUDA_HOME=/usr/local/cuda

# Confirm
$ ncvv -V

# Restart server
$ sudo reboot
```

# cuDNN 7.6.5 upgrade
1. Go to the cuDNN download page (need registration) and select the latest cuDNN 7.6.5 version made for CUDA 10.2. Download the 3 deb file for the ubuntu18.04 and go to the download folder and install from there.
2. Install files
```
# first install the runtime library
$ sudo dpkg -i libcudnn7_7.6.5.32-1+cuda10.2_amd64.deb

# then developer library
$ sudo dpkg -i libcudnn7-dev_7.6.5.32-1+cuda10.2_amd64.deb

# last the sample codes
$ sudo dpkg -i libcudnn7-doc_7.6.5.32-1+cuda10.2_amd64.deb

# check
$ dpkg -l | grep cudnn
```
