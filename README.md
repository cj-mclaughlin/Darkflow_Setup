## Install Scripts for Remote Servers (Ubuntu)
First, clone and go into the script directory
```
git clone https://github.com/cj-mclaughlin/Darkflow_Setup && cd Darkflow_Setup/Install
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
Go into the Cuda directory and run the script.
Use -r flag option to remove all previous nvidia drivers/files.
```
cd Cuda && sudo ./install_cuda (-r)
```

### cuDNN
We cannot install secure cuDNN files over wget, so the files must be downloaded from their website.
I have included the most recent version (as of 6/11/2019) in this repository.
```
cd cuDNN && sudo ./install_cuda
```
