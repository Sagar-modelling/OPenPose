# OpenPose
Installing OpenPose with CUDA 10.1 and cuDNN for Ubuntu 18.04

# Update and upgrade your system
```
sudo apt-get update
sudo apt-get upgrade
```

# Install the lastest NVIDIA driver for your system using “Software & Updates”
```
After installation reload system. Verify that driver installed successfully using command nvidia-smi
```
# Install cmake-gui
```
Ubuntu 18: Download and compile CMake-gui from source. The default CMake-gui version (3.10) installed via sudo apt-get install cmake-qt-gui provokes some compiling errors. Required CMake version >= 3.12.
Uninstall your current Cmake-gui version by running sudo apt purge cmake-qt-gui.
Install OpenSSL for building CMake by running sudo apt install libssl-dev.
Run sudo apt-get install qtbase5-dev.
Download the Latest Release of CMake Unix/Linux Source from the CMake download website, called cmake-X.X.X.tar.gz.(https://cmake.org/download/)
Unzip it and go inside that folder from the terminal.
Run ./configure --qt-gui. Make sure no error occurred.
Run ./bootstrap && make -j`nproc` && sudo make install -j`nproc`. Make sure no error occurred.
Assuming your CMake downloaded folder is in {CMAKE_FOLDER_PATH}, every time these instructions mentions cmake-gui, you will have to replace that line by {CMAKE_FOLDER_PATH}/bin/cmake-gui

```
#  CUDA installation
```
Go to official website NVIDIA for CUDA 10.1 (https://developer.nvidia.com/cuda-10.1-download-archive-base). 
sudo sh cuda_10.1.105_418.39_linux.run
After successfull installation add paths for CUDA to your bashrc file
sudo nano ~/.bashrc

Add those lines to the end of file:
export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
After that, save file and run
source ~/.bashrc
```

# cuDNN 7.5.1 Download
```
(https://developer.nvidia.com/rdp/cudnn-archive). Log in or register there.
Choose Download cuDNN v7.5.1 (April 22, 2019), for CUDA 10.1.

After downloading unzip that cudnn-10.1-linux-x64-v7.5.1.10.tgz
Then just copy those files to your cuda directory using those commands
sudo cp cuda/include/cudnn.h /usr/local/cuda/include/
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64/

Add permisions
sudo chmod a+r /usr/local/cuda/include/cudnn.h
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```
# Installing other OpenPose prerequisites
```
conda create -n openpose python=3.7 -y
sudo apt-get install libopencv-dev
mkdir openpose_folder
In openpose_folder git clone OpenPose
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose.git

Install Caffe prerequisites.
Go to OpenPose folder and run install_deps.sh
cd openpose
sudo bash ./scripts/ubuntu/install_deps.sh

Now build Caffe from source for Openpose
cd 3rdparty
git clone https://github.com/CMU-Perceptual-Computing-Lab/caffe.git

sudo apt-get install python3-dev
sudo pip3 install numpy opencv-python

Create an empty subcategory “build” folder inside Openpose folder
mkdir build

start CMake GUI
select “Browse Source” => Choose your OpenPose directory, then select “Browse Build” => Choose OpenPose/build folder
Select Configure to compile the files. A dialog box appears CMakeSetup.
Choose Unix Makefiles and Use defaults native compilers
After successful configuration, check the “BUILD_PYTHON” inside the red box
Now click “Generate”
After ending of generation, close CMake.

Open terminal, go to build folder
cd openpose/build/
make -j`nproc`
Compile the Openpose source
sudo make install

Compile and build the python Openpose
cd openpose/build/python/openpose
sudo make install
```
# Testing

```
cd openpose/build/examples/tutorial_api_python
python3 01_body_from_image.py

For Python API error: Cannot import name pyopenpose
https://github.com/CMU-Perceptual-Computing-Lab/openpose/issues/1027

```


