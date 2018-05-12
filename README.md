# Caffe-Installation-Ubuntu-16.04-cuda-9.0-cudnn-v7

Installing Caffe on a fresh-installed ubuntu 16.04 (please fully update ubuntu software first), with cuda 9.0 and cudnn v7.

**1. Install NVIDIA driver.**
      
      sudo add-apt-repository ppa:graphics-drivers/ppa
      sudo apt-get update  
      sudo apt-get install nvidia-384 (check the gpu drive number on NVIDIA website, and change it to fit your GPU. E.x., 384 is for Titan X)  
      sudo shutdown -r now  


**2. Install CUDA 9.0.**\
            Download cuda 9.0 from (https://developer.nvidia.com/cuda-90-download-archive)
            
      cd ~/Downloads
      sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb
      sudo apt-get update
      sudo apt-get install cuda
      echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.bashrc
      echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc

compile cuda samples, open a new terminal:

      cuda-install-samples-9.0.sh ~/cuda-samples
      cd ~/cuda-samples/NVIDIA*Samples
      make -j $(($(nproc) + 1))
      sudo shutdown -r now
      
check cuda installation, open a new terminal:

      cd ~/cuda-samples/NVIDIA*Samples
      bin/x86_64/linux/release/deviceQuery
      bin/x86_64/linux/release/bandwidthTest

**3. Install CUDNN v7.**\
      Download cudnn v7 from (https://developer.nvidia.com/cudnn)
            
      cd ~/Downloads/
      tar xvf cudnn*.tgz
      cd cuda
      sudo cp */*.h /usr/local/cuda/include/
      sudo cp */*.so* /usr/local/cuda/lib64/

**4. Install Anaconda.**\
      Download Anaconda from (https://www.anaconda.com/download/#linux)
            
      cd ~/Downloads
      bash Anaconda*.sh

Log out and log in again to activate the new variables (close and open the terminal).


**5. Install other dependencies.**

      sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
      sudo apt-get install --no-install-recommends libboost-all-dev
      sudo apt-get install libopenblas-dev
      sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
      
create symbolic link for hdf5:

      cd /usr/lib/x86_64-linux-gnu
      sudo ln -s libhdf5_serial.so.10.1.0 libhdf5.so
      sudo ln -s libhdf5_serial_hl.so.10.0.2 libhdf5_hl.so

**6. Download Caffe.**
open a new terminal,

      git clone https://github.com/BVLC/caffe
      
download and copy the attached Makefile.config into caffe folder


**7. Build Caffe.**\
open a terminal in caffe folder

      make all -j $(($(nproc) + 1))
      make test -j $(($(nproc) + 1))
      make runtest -j $(($(nproc) + 1))
      pip install protobuf
      make pycaffe -j $(($(nproc) + 1))
      echo "export CAFFE_ROOT=$(pwd)" >> ~/.bashrc
      echo 'export PYTHONPATH=$CAFFE_ROOT/python:$PYTHONPATH' >> ~/.bashrc
      conda install libgcc

**8. Test the Caffe installation.**\
open a new terminal

      python
      import caffe
      
Cheers!\
\
Feel free to contact me at (yixindu1573@gmail.com) for any questions.














































      



