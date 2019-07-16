## Install Scripts for Remote Servers (Ubuntu)
This repo was made for setting up darkflow on AWS ubuntu servers. I use AWS S3 to fetch CUDA/cuDNN deps, so make sure you have AWS-CLI installed. If modifying these scripts on windows, you may have to run `dos2unix <script_name>` before it is able to run on your server, or change the line terminator from CRLF to LF in your text editor/ide.
```
pip3 install awscli --upgrade --user
```

First, clone and go into the script directory. (change permissions as needed)
```
git clone https://github.com/cj-mclaughlin/Darkflow_Setup.git && chmod +x -R Darkflow_Setup
cd Darkflow_Setup
```

### OpenCV
Run install_opencv. Defaults to OpenCV4 but reads in the first argument as a version.
Current version of darkflow requires OpenCV3, so using 3.4 as an argument is recommended.
Default installation:
```
cd OpenCV && sudo ./install_opencv
```
With option (for version 3.4):
```
cd OpenCV && sudo ./install_opencv 3.4
```

### Cuda
Instead of installing Cuda over wget (due to automatic 10.1 patches), the script downloads a local .deb from an aws S3 bucket. 
Use -r flag option to remove all previous drivers/files.
```
cd Cuda && sudo ./install_cuda (-r)
```

### cuDNN
Install script automatically grabs .tgz install file from the aforementioned S3 bucket.
```
cd cuDNN && sudo ./install_cuda
```

### Tensorflow
Current script installs tensorflow 1.13.1 over pip; if wanting to build from source I have included bazel v0.21 install script in the flow directory, and then you can install tensorflow from source following the guidelines [here](https://www.tensorflow.org/install/source#download_the_tensorflow_source_code). Remember sure to run `git checkout v1.13.1` or `git checkout v1.13.2` from the root of the tensorflow directory after cloning the repo. 

This script also clones the darkflow repository and installs it locally with pip.
```
cd Flow && sudo ./install_darkflow
```

### Verify Installation
OpenCV installation can be verified with one of the following, depending on your version.
```
pkg-config --modversion opencv
pkg-config --modversion opencv3
pkg-config --modversion opencv4
```
Cuda can be verified through `nvidia-smi` and to check if cuDNN added its files try:
```
CUDNN_H_PATH=/usr/local/cuda/include/cudnn.h
cat ${CUDNN_H_PATH} | grep CUDNN_MAJOR -A 2
```
Tensorflow and Darkflow should be tested on a sample production dataset, if available.

### Future plans
Move off of AWS S3 for storage and onto github LFS.
