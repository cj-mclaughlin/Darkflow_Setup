## Install Scripts for Remote Servers (Ubuntu)
This repo was made for setting up darkflow on AWS ubuntu servers. I use AWS S3 to fetch CUDA/cuDNN deps, so make sure you have AWS-CLI installed. If you edit any of these scripts on windows, make sure to change your line endings to LF (as opposed to CRLF), or run the scripts through `dos2unix <script-name>` first. 
```
pip3 install awscli --upgrade --user
```

First, clone and go into the script directory
```
git clone https://github.com/cj-mclaughlin/Darkflow_Setup && cd Darkflow_Setup
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

### Installation Verification
OpenCV installation can be verified with one of the following, depending on your version.
```
pkg-config --modversion opencv
pkg-config --modversion opencv3
pkg-config --modversion opencv4
```
Cuda/Cudnn can be verified through:
```
nvidia-smi
nvcc --version
```
Tensorflow and Darkflow should be tested on a sample production dataset, if available.

### Future plans
Follow-up testing.
Move off of AWS S3 for storage and onto github LFS.