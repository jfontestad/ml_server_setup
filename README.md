# ml_server_setup

#INSTALL UBUNTU

#INSTALL NVIDIA DRIVERS

Verify the system has gcc installed
For development using the CUDA, you need to make sure gcc is installed. You can check if it's installed using the command:

$ gcc --version
If not installed, install it with apt-get as below:

$ sudo apt install gcc-6 g++-6

Verify the system has the correct kernel headers and development packages installed.

The CUDA Driver requires that the kernel headers and development packages for the running version of the kernel be installed at the time of the driver installation, as well whenever the driver is rebuilt. You can install kernel headers and development tools using:

$ sudo apt-get install linux-headers-$(uname -r)
Install NVIDIA Driver
CUDA needs Nvidia driver installed on your machine. Install it on Ubuntu 18.04 using the command:

$ sudo apt install nvidia-384
Once this has been installed, you can proceed to install Nvidia CUDA toolkit.

Download the NVIDIA CUDA Toolkit
Depending on your installation method of choice, you need to download equivalent package.  I prefer installing CUDA from a runfile on Ubuntu 18.04 since it is hard to encounter dependency issues.

As of this writing, the latest release of CUDA is v9.2. Since the package size is above 1GB, I'll use wget command to download it so that I can resume easily if the connection gets broken. The CUDA Toolkit contains the CUDA driver and tools needed to create, build and run a CUDA application as well as libraries, header files, CUDA samples source code, and other resources.

$ cd Dowloads
$ wget -c https://developer.nvidia.com/compute/cuda/9.2/Prod/local_installers/cuda_9.2.88_396.26_linux
Once the package has been downloaded locally, make it executable and install it.

# chmod +x cuda_9.2.88_396.26_linux.run
# ./cuda_9.2.88_396.26_linux.run --verbose --silent --toolkit --override
You should get output similar to below on complete installation.

===========
= Summary =
===========

Toolkit: Installed in /usr/local/cuda-9.2
Samples: Not Selected

Please make sure that
 - PATH includes /usr/local/cuda-9.2/bin
 - LD_LIBRARY_PATH includes /usr/local/cuda-9.2/lib64, or, add /usr/local/cuda-9.2/lib64 to /etc/ld.so.conf and run ldconfig as root
Modify your .bashrc file to include Cuda bin in its path:

export PATH="$PATH:/usr/local/cuda-9.2/bin"
Ensure CUDA library path is present.

# echo "/usr/local/cuda-9.2/lib64" >> /etc/ld.so.conf
# ldconfig
Check https://developer.nvidia.com/cuda-downloads for available patches and download the .run file then install it.

# wget https://developer.nvidia.com/compute/cuda/9.2/Prod/patches/1/cuda_9.2.88.1_linux
# chmod +x cuda_9.2.88.1_linux.run
# ./cuda_9.2.88.1_linux.run --silent --accept-eula

Welcome to the CUDA Patcher.
Installation complete!
Installation directory: /usr/local/cuda-9.2
Create symlinks to GCC6 in the CUDA bin folder:

# ln -s /usr/bin/gcc-6 /usr/local/cuda-9.2/bin/gcc
# ln -s /usr/bin/g++-6 /usr/local/cuda-9.2/bin/g++
