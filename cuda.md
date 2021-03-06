### Pre-installation actions
1. Verify the system has a CUDA-capable GPU
```
lspci | grep -i nvidia
```

2. Verify the system is running a supported version of Linux.
```
uname -m && cat /etc/*release
```

3. Verify the system has gcc installed.
```
gcc --version
```

3. Verify the system has the correct kernel headers and development packages installed.
```
uname -r
```

4. install the header if not available
```
sudo apt-get install linux-headers-$(uname -r)
```

5. checksum
```
md5sum <file>
```

6. Download the NVIDIA CUDA Toolkit
```
https://developer.nvidia.com/cuda-downloads
```
For Ubuntu 16.04, the downloaded file should be:
```
cuda-repo-ubuntu1404_7.5-18_amd64.deb
```

7. to check nvidia
```
nvidia-settings
```

###### Download sites
```
http://developer.download.nvidia.com/compute/cuda/repos/
https://developer.nvidia.com/cuda-downloads
```

### install from packages
* Package Manager (Ubuntu)
* install the downloaded deb file
```
sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb
e.g. sudo dpkg -i cuda-repo-ubuntu1404_7.5-18_amd64.deb
```

```
sudo apt-get update
sudo apt-get install cuda
```

* optional: cuda dev library (??)
```
sudo apt-get install -y cuda
```

* ubuntu repository
```
sudo apt install nvidia-cuda-dev nvidia-cuda-toolkit
```

* alternatively, install from run file
```
sudo sh cuda_xxx_linux.run
```

### post-installation
1. edit .profile file
```
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```
optional:
```
export CUDA_HOME=/usr/local/cuda-8.0
PATH=${CUDA_HOME}/bin:${PATH} 
export PATH
```

2. install writable samples
```
cuda-install-samples-7.5.sh <dir>
e.g. ~/FraDir/cuda_samples
```
In order to modify, compile, and run the samples, the samples must be installed with write permissions

3. check the driver version
```
cat /proc/driver/nvidia/version
NVRM version: NVIDIA UNIX x86_64 Kernel Module  367.57  Mon Oct  3 20:37:01 PDT 2016
GCC version:  gcc version 5.4.0 20160609 (Ubuntu
5.4.0-6ubuntu1~16.04.4)
```

4. check CUDA Toolkit version
```
nvcc -V
```

5. compile the samples
```
cd <dir>/NVIDIA_CUDA-8.0_Samples && make
```

6. To verify installation with CUDA SDK samples
```
cd <dir>/NVIDIA_CUDA-8.0_Samples 
./deviceQuery 
```

###### Sample Outupt
```
 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "GeForce GT 750M"
  CUDA Driver Version / Runtime Version          8.0 / 8.0
  CUDA Capability Major/Minor version number:    3.0
  Total amount of global memory:                 2000 MBytes (2097676288 bytes)
  ( 2) Multiprocessors, (192) CUDA Cores/MP:     384 CUDA Cores
  GPU Max Clock rate:                            967 MHz (0.97 GHz)
  Memory Clock rate:                             2005 Mhz
  Memory Bus Width:                              128-bit
  L2 Cache Size:                                 262144 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 1 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 4 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 8.0, CUDA Runtime Version = 8.0, NumDevs = 1, Device0 = GeForce GT 750M
Result = PASS
```

Bandwidth Test
```
cd <cuda_samples folder>/NVIDIA_CUDA-8.0_Samples/bin/x86_64/linux/release
./bandwidthTest
```
Sample Output
```
 Device 0: GeForce GT 750M
 Quick Mode

 Host to Device Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(MB/s)
   33554432			1496.1

 Device to Host Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(MB/s)
   33554432			1567.2

 Device to Device Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(MB/s)
   33554432			45181.0

Result = PASS
```

###### Others (not used)
```
apt-get install nvidia-cuda-toolkit
```

setup GPU and CUDA
```
sudo wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1404/x86_64/cuda-repo-ubuntu1404_6.5-14_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1404_6.5-14_amd64.deb
sudo apt-get update
sudo apt-get install -y cuda # this takes a while
echo -e "\nexport PATH=/usr/local/cuda-6.5/bin:$PATH\n\nexport LD_LIBRARY_PATH=/usr/local/cuda-6.5/lib64" >> .bashrc
sudo reboot
```

### Uninstall
Use the following command to uninstall a Toolkit runfile installation:
```
sudo /usr/local/cuda-X.Y/bin/uninstall_cuda_X.Y.pl
```

Use the following command to uninstall a Driver runfile installation:
```
sudo /usr/bin/nvidia-uninstall
```

Use the following commands to uninstall a RPM/Deb installation:
```
sudo yum remove <package_name>                      # Redhat/CentOS
sudo dnf remove <package_name>                      # Fedora
sudo zypper remove <package_name>                   # OpenSUSE/SLES
sudo apt-get --purge remove <package_name>          # Ubuntu
```

### install cuDNN
1. Check CUDA location
```
ldconfig -p | grep cuda
```

2. Download and extract

3. copy to the CUDA directory
```
tar xvzf cudnn-8.0-linux-x64-v5.1.tgz
cd cuda
sudo cp include/cudnn.h /usr/local/cuda-8.0/include/
sudo cp lib64/* /usr/local/cuda-8.0/lib64/
```

4. usage
    * <installpath> is /usr/local/cuda-8.0/lib64/
    * Add <installpath> to your build and link process by adding -I<installpath> to your compile
line and -L<installpath> -lcudnn to your link line.


###### install Bazel (Optional)
```
echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
curl https://storage.googleapis.com/bazel-apt/doc/apt-key.pub.gpg | sudo apt-key add -
sudo apt-get update && sudo apt-get install bazel
sudo apt-get upgrade bazel
```


###### install caffe
```
git clone https://github.com/BVLC/caffe.git
cd caffe/python/
for req in $(cat requirements.txt); do sudo -H pip install $req --upgrade; done
sudo -H pip install python-dateutil --upgrade
```

###### linux basic dependency
```
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get install --no-install-recommends libboost-all-dev
```

###### BLAS
```
sudo apt-get install libatlas-base-dev
```


###### Edit the make file
* Copy make file
```
cp Makefile.config.example Makefile.config
```

* For CPU & GPU accelerated Caffe, no changes are needed.
* For cuDNN acceleration using NVIDIA’s proprietary cuDNN software, uncomment the 
```
USE_CUDNN := 1 
```
switch in Makefile.config. 
* cuDNN is sometimes but not always faster than Caffe’s GPU acceleration.

* uncomment:
```
USE_CUDNN := 1
WITH_PYTHON_LAYER := 1
```

* TODO: ckeck -- change:
```
CUDA_DIR := /usr/local/cuda-8.0
```

* default is python 2
```
PYTHON_INCLUDE := /usr/include/python2.7 /usr/lib/python2.7/dist-packages/numpy/core/include
```
* to switch to python 3
```
PYTHON_LIBRARIES := boost_python-py35 python3.5m
PYTHON_INCLUDE := /usr/include/python3.5m /usr/lib/python3.5/dist-packages/numpy/core/include
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/hdf5/serial
```

* to compile, adjust Makefile.config (for example, if using Anaconda Python, or if cuDNN is desired)
```
make all
make test
make runtest
```

* to compile the python wrappers
```
make pycaffe
```

* set python path in .profile
```
export PYTHONPATH=/path/to/caffe/python:$PYTHONPATH
```

### install Theano
1. Install
```
sudo apt-get install python-numpy python-scipy python-dev python-pip python-nose g++ libopenblas-dev git
sudo -H pip install nose2 nose-parameterized
sudo pip install Theano
```

2. check config
```
python3 -c 'import theano; print(theano.config)' | less
```

3. testing (for python 2)
```
nosetests theano
```

4. configurations
```
Create ~/.theanorc file with the following content:
       [global]
       device = gpu
       floatX = float32

       [lib]
       cnmem = 0.7

       #[blas]
       #ldflags = -L /usr/local/lib -lopenblas

       [nvcc]
       fastmath = True
       #flags=-D_FORCE_INLINES
       [cuda]
       root = /usr/local/cuda-8.0
```

5. run tests
Run python test_theano.py

```
from theano import function, config, shared, sandbox
import theano.tensor as T
import numpy
import time            
vlen = 10 * 30 * 768  # 10 x #cores x # threads per core
iters = 1000            
rng = numpy.random.RandomState(22)
x = shared(numpy.asarray(rng.rand(vlen), config.floatX))
f = function([], T.exp(x))
print (f.maker.fgraph.toposort())
t0 = time.time()
for i in range(iters):
    r = f()
t1 = time.time()
print ('Looping %d times took' % iters, t1 - t0, 'seconds')
print ('Result is', r)
if numpy.any([isinstance(x.op, T.Elemwise) and 
            ('Gpu' not in type(x.op).__name__) 
            for x in f.maker.fgraph.toposort()]):
    print('Used the cpu')
else:
    print('Used the gpu')

```

### Tensorflow
1. install dependencies
```
sudo apt-get install libcupti-dev
```

2. need pip version 8.1 or later
```
#pip install tensorflow (cpu)
pip install tensorflow-gpu
```

3. testing tensorflow
```
cd tensorflow/models/image/mnist
python convolutional.py
```
Start and close a session:
```
import tensorflow as tf
sess = tf.InteractiveSession()
sess.close()
```
Do some calculations
```
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
a = tf.constant(10)
b = tf.constant(32)
print(sess.run(a + b))
```

### Deep Learning libraries
Keras
```
sudo pip3 install keras
```

###### others (not used)
* Configure and build openblas:
```
sudo apt-get install gfortran
git clone https://github.com/xianyi/OpenBLAS
cd OpenBLAS
make FC=gfortran
sudo make PREFIX=/usr/local install
```

alternatively	
```
sudo pip install --upgrade --no-deps git+git://github.com/Theano/Theano.git
echo -e "\n[global]\nfloatX=float32\ndevice=gpu\n[mode]=FAST_RUN\n\n[nvcc]\nfastmath=True\n\n[cuda]\nroot=/usr/local/cuda" >> ~/.theanorc
```

* ubuntu 16.04 with cuda 8 only


* cuda 7.5 don't support the default g++ version. Install an supported version and make it the default.
```
sudo apt-get install g++-4.9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 20
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 10
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 10
sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 30
sudo update-alternatives --set cc /usr/bin/gcc
sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 30
sudo update-alternatives --set c++ /usr/bin/g++
```

* Work around a glibc bug
echo -e "\n[nvcc]\nflags=-D_FORCE_INLINES\n" >> ~/.theanorc


