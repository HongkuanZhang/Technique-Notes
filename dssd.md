# Cuda10.2 upgrade

1.事前準備
```
#既にドライバーがインストールされていないかチェックする
$ dpkg -l | grep nvidia 
$ dpkg -l | grep cuda
```

2.古いcudaとDriverをアンインストール
```
$ sudo apt-get --purge remove nvidia-*
$ sudo apt-get --purge remove cuda-*
$ sudo rm -rf /usr/local/cuda* 
```

3.リポジトリを登録
```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
```

4.ドライバーのインストール
```
$ ubuntu-drivers devices # 推奨ドライバーのバージョンを確認
$ sudo apt install nvidia-driver-440  nvidia-settings
$ sudo reboot
$ nvidia-smi  # GPUが認識されているかを確認
```

5.NVIDIAのウェブからCuda10.2をインストール
```
# Select Target Platform
Operating system: Linux
Architecture: x86_64
Distribution: ubuntu
Version: 16.04
Install type: dev(local)

# Install according to the commands provided by official site
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
$ sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
$ wget http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb
$ sudo dpkg -i cuda-repo-ubuntu1804-10-2-local-10.2.89-440.33.01_1.0-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-10-2-local-10.2.89-440.33.01/7fa2af80.pub
$ sudo apt update
$ sudo apt -y install cuda

# add path in .bashrc
$ echo 'export PATH=/usr/local/cuda-10.2/bin${PATH:+:${PATH}}' >> ~/.bashrc
$ echo 'export LD_LIBRARY_PATH=/usr/local/cuda-10.2/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}' >> ~/.bashrc
$ source ~/.bashrc
$ sudo ldconfig

# Confirm
$ ncvv -V
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
