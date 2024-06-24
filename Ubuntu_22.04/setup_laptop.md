# nvidia-driver-545 & CUDA-12.3 install
* Install nvidia driver 545
* Install cuda-12.3.2
* Install cudnn 8.9.7.29
* install opencv cuda build

## Install nvidia driver 545

~~~
sudo lshw -numeric -C display
sudo apt-get purge nvidia*
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
sudo apt upgrade
ubuntu-drivers list
sudo apt install nvidia-driver-545
reboot
~~~

## Install cuda-12.3.2

~~~
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin

sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.3.2/local_installers/cuda-repo-ubuntu2204-12-3-local_12.3.2-545.23.08-1_amd64.deb

sudo dpkg -i cuda-repo-ubuntu2204-12-3-local_12.3.2-545.23.08-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-3-local/cuda-*-keyring.gpg /usr/share/keyrings/

sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3

sudo nano ~/.bashrc
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
source ~/.bashrc
~~~

## Install cudnn 8.9.7.29

* unzip cudnn-linux-x86_64-8.9.7.29
~~~
tar -xvf cudnn-linux-x86_64-8.9.7.29_cuda12-archive.tar.xz
~~~

* capy cudnn lib
~~~
sudo cp cudnn-linux-x86_64-8.9.7.29_cuda12-archive/include/cudnn*h /usr/local/cuda-12.3/include

sudo cp cudnn-linux-x86_64-8.9.7.29_cuda12-archive/lib/libcudnn* /usr/local/cuda-12.3/lib64

sudo chmod a+r /usr/local/cuda-12.3/include/cudnn*.h /usr/local/cuda-12.3/lib64/libcudnn*
~~~  

## install opencv cuda build

### install dependencies

* install cmake
~~~
sudo apt install cmake
~~~

* install gcc g++
~~~
sudo apt install gcc g++
sudo apt install build-essential
~~~

* install python3, python-devel and Numpy
~~~~
sudo apt install python3 python3-dev python3-numpy
~~~~

* install GTK is requried for GUI features, Camera support (v4l), Media Support
~~~
sudo apt install libavcodec-dev libavformat-dev libswscale-dev
sudo apt install libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev 
sudo apt install libgtk-3-dev
~~~

* intall dependencies support for PNG, JPEG, JPEG2000, TIFF, WebP, etc  formats

~~~
sudo apt install libpng-dev libjpeg-dev libopenexr-dev libtiff-dev libwebp-dev
~~~

* Download Opencv
~~~
git clone https://github.com/opencv/opencv.git
~~~

* Download OpenCV-contrib
~~~
git clone https://github.com/opencv/opencv_contrib.git
~~~

* check mount gpu model
~~~
nvidia-smi -L
~~~

* create build directory
~~~
cd ~/opencv
mkdir build
cd build
~~~

* cmake opencv cuda 
~~~
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_CUDA=ON -D WITH_CUDNN=ON -D WITH_CUBLAS=ON -D WITH_TBB=ON -D OPENCV_DNN_CUDA=ON -D OPENCV_ENABLE_NONFREE=ON -D CUDA_ARCH_BIN=6.1 -D OPENCV_EXTRA_MODULES_PATH=$HOME/opencv_contrib/modules -D BUILD_EXAMPLES=OFF -D HAVE_opencv_python3=ON ..
~~~

~~~
make -j4
~~~

* build opencv
~~~
sudo make install
~~~

