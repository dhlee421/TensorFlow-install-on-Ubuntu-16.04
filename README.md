# TensorFlow Setup on Ubuntu 16.04

**After Install Linux, Upgrade the packages** <br />
sudo apt-get update <br />
sudo apt-get upgrade<br />

**Install nvidia device driver**
sudo apt-add-repository -y ppa:graphics-drivers/ppa
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install nvidia-current nvidia-settings

[System Settings]-[Software & Updates]-[Additional Drivers]
+— NVIDIA Corporation:Unknown
+— Using NVIDIA binary driver-version 367.35 from nvidia-367(open source)

**Install CUDA and cuDNN**
sudo apt-get install libglu1-mesa libxi-dev libxmu-dev libglu1-mesa-dev
sudo sh cuda_8.0.27_linux.run –override

tar -xvzf cudnn-8.0-linux-x64-v5.0-ga.tgz
sudo cuda/include/cudnn.h /usr/local/cuda/include/
sudo cp cuda/include/cudnn.h /usr/local/cuda/include/
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*

export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH

**Python Module install**
sudo apt-get install swig

sudo apt-get install python3-pip
sudo apt-get install python-pip

pip3 install -upgrade pip
pip install -upgrade pip

sudo apt-get install python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-dev

sudo apt-get install python3-numpy python3-scipy python3-matplotlib ipython3 ipython3-notebook python3-pandas python3-sympy python3-dev

Install bazel

sudo apt-get install python-software-properties
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
./bazel-0.3.0-installer-linux-x86_64.sh –user

export PATH=/home/oneway/bin:$PATH
edit .bashrc
add following line to end of the file
source /home/oneway/.bazel/bin/bazel-complete.bash

Install early version of gcc/g++
sudo apt-get install zlib1g-dev
sudo apt-get install libc6-dev <>
sudo apt-get install gcc-4.9
sudo apt-get install g++-4.9
sudo update-alternatives –remove-all gcc
sudo update-alternatives –install /usr/bin/gcc gcc /usr/bin/gcc-4.9 10
sudo update-alternatives –install /usr/bin/g++ g++ /usr/bin/g++-4.9 10

Compile TensorFlow
bazel clean
bazel build -c opt –config=cuda //tensorflow/cc:tutorials_example_trainer
bazel-bin/tensorflow/cc/tutorials_example_trainer –use_gpu

bazel build -c opt –config=cuda //tensorflow/tools/pip_package:build_pip_package
bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg

sudo pip install /tmp/tensorflow_pkg/tensorflow-0.9.0-py2-none-any.whl

sudo pip3 install /tmp/tensorflow_pkg/tensorflow-0.9.0-py3-none-any.whl
