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

### TF/Darkflow
Tensorflow/Darkflow is more percise, so the installation script is more of a guideline and I am not certain everything will run perfectly on your machine. Look through the script walk through it line-by-line if something goes wrong.
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
