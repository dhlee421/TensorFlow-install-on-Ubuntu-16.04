# System Specification 

CPU: 6th i7 Skylake 6700<br />
Mother Board: Gigabyte Z170X-DESIGNARE<br />
Graphic Card: GEFORCE GTX-1080 x2<br />
Memory: 32G<br />
SSD: 256×2<br />
HDD: 2Tx2<br />
<br />
OS: Linux ( Ubuntu 16.04)<br />
<br />
# TensorFlow Setup on Ubuntu 16.04

**After Install Linux, Upgrade the packages** <br />
```
sudo apt-get update
sudo apt-get upgrade
```

**Install nvidia device driver**<br />
```
sudo apt-add-repository -y ppa:graphics-drivers/ppa
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install nvidia-current nvidia-settings
```
<br />
```
[System Settings]-[Software & Updates]-[Additional Drivers]
+— NVIDIA Corporation:Unknown
+— Using NVIDIA binary driver-version 367.35 from nvidia-367(open source)
```
<br />
**Install CUDA and cuDNN**<br />
```
sudo apt-get install libglu1-mesa libxi-dev libxmu-dev libglu1-mesa-dev
sudo sh cuda_8.0.27_linux.run –override
```
<br />
```
tar -xvzf cudnn-8.0-linux-x64-v5.0-ga.tgz
sudo cuda/include/cudnn.h /usr/local/cuda/include/
sudo cp cuda/include/cudnn.h /usr/local/cuda/include/
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn(star)
```
<br />
`export PATH=/usr/local/cuda/bin:$PATH`<br />
`export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH`<br />
<br />
**Python Module install**<br />
```
sudo apt-get install swig
```
<br />
```
sudo apt-get install python3-pip
sudo apt-get install python-pip
```
<br />
```
pip3 install -upgrade pip
pip install -upgrade pip
```
<br />
```
sudo apt-get install python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-dev
```
<br />
```
sudo apt-get install python3-numpy python3-scipy python3-matplotlib ipython3 ipython3-notebook python3-pandas python3-sympy python3-dev
```
<br />
**Install bazel**<br />
<br />
```
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
./bazel-0.3.0-installer-linux-x86_64.sh –user
```
<br />
```
export PATH=/home/oneway/bin:$PATH
```
edit .bashrc<br />
__add following line to end of the file__<br />
```
source /home/oneway/.bazel/bin/bazel-complete.bash
```
<br />
**Install early version of gcc/g++**<br />
```
sudo apt-get install zlib1g-dev
sudo apt-get install libc6-dev
sudo apt-get install gcc-4.9
sudo apt-get install g++-4.9
sudo update-alternatives –remove-all gcc
sudo update-alternatives –install /usr/bin/gcc gcc /usr/bin/gcc-4.9 10
sudo update-alternatives –install /usr/bin/g++ g++ /usr/bin/g++-4.9 10
```
<br />
**Compile TensorFlow**<br />
```
bazel clean
bazel build -c opt –config=cuda //tensorflow/cc:tutorials_example_trainer
bazel-bin/tensorflow/cc/tutorials_example_trainer –use_gpu
```
<br />
```
bazel build -c opt –config=cuda //tensorflow/tools/pip_package:build_pip_package
bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```
<br />
```
sudo pip install /tmp/tensorflow_pkg/tensorflow-0.9.0-py2-none-any.whl
```
<br />
```
sudo pip3 install /tmp/tensorflow_pkg/tensorflow-0.9.0-py3-none-any.whl
```
