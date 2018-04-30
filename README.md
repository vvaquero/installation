# Install Stuff For Deep Learning
Notes to install stuff need for Deep Learning. Maybe also other stuff as Latex, in case I get bored. 

# Table of contents
1. [Nvidia](#Nvidia)
2. [Pytorch Virtual Environment](#Pytorch_venv)
3. [TensorFlow Virtual Environment](#TensorFlow_venv)
4. [Python3 Virtual Environment](#python3_venv)
5. [Install Docker and Nvidia-Docker](#docker)
6. [Ubuntu Tweaks](#tweaks)

Nvidia <a name="Nvidia"></a>
======

Up to Feb 2018, I update to Cuda 9.0 (9.1 is not still compatible to everything)

### Driver Nvidia
* It is better to install Nvidia driver from Ubuntu repository to let it update automatically. In this way, upgrading ubuntu will, given the case, upgrade the driver without problem

```sudo apt-get install nvidiaXXX```

### CUDA & CUDNN
* To install CUDA library, download the BINARY -runfile(local) file from the Nvidia website:  
https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=runfilelocal

* Give the file executable permisions, and execute it to install the library.  
```chmod +x cuda_9.0.176.1_linux.run```  
``` cuda_9.0.176.1_linux.run```   
**IMPORTANT:** when the installation ask you to install the driver, select **NO** (we do not want an static driver installation). You can select to do a symbolic link (would be under the name of cuda directly), or alternatively keep several cuda versions and link each framework directly to the desired one (to the folder cuda-X.X)

* Download CUDNN library from the Nvidia website (you need to be registered)  
https://developer.nvidia.com/cudnn  
Copy the files inside the cudnn lib64 folder to the corresponding cuda folder ```/usr/local/cuda-9.0/lib64```. 
Copy the files inside the cudnn include folder to the corresponding cuda folder ```/usr/local/cuda-9.0/include```. 



Pytorch in a Virtual Environment <a name="Pytorch_venv"></a>
======

* Create install and create the virtual environment  
```sudo apt-get install python-pip python-dev python-virtualenv```  
```mkdir ~/virtualenv/```  
* Launch a venv for pytorch and source it  
```virtualenv --system-site-packages ~/virtualenv/pytorch/```  
```source ~/virtualenv/pytorch/bin/activate```  
* Install pytorch stuff in the venv created  
```pip install numpy scipy matplotlib scikit-image scikit-learn ipython protobuf jupyter tqdm ipykernel```  
Get the link from the pytorch web (e.g options: linux, pip, python 2.7, cuda 9.0  
```pip install <link http://pytorch.org/>```  
```pip install torchvision```  
```python -m ipykernel install --user --name=numpy```  
* Add the path to bash  
```echo "alias pytorch='source ~/virtualenv/pytorch/bin/activate'" >> ~/.bashrc```  
```deactivate```  
* Execution  
**to activate:**   
```pytorch```  
**to deactivate:**  
```deactivate```


TensorFlow in a Virtual Environment <a name="TensorFlow_venv"></a>
======

* Create install and create the virtual environment  
```sudo apt-get install python-pip python-dev python-virtualenv```  
```mkdir ~/virtualenv/```  
* Launch a venv for TensorFlow and source it  
```virtualenv --system-site-packages ~/virtualenv/tensorflow/```  
```source ~/virtualenv/tensorflow/bin/activate```  
* Install pytorch stuff in the venv created  
```pip install numpy scipy matplotlib scikit-image scikit-learn ipython protobuf jupyter tqdm ipykernel```  
```pip install tensorflow-gpu```  
```python -m ipykernel install --user --name=tensorflow```  
* Add the path to bash  
```echo "alias tensorflow='source ~/virtualenv/tensorflow/bin/activate'" >> ~/.bashrc```  
```deactivate```  
**to activate:**   
```tensorflow```  
**to deactivate:**  
```deactivate```



Get a Python-3 Virtual Environment <a name="python3_venv"></a>
======

```sudo apt-get install python3-pip python3-dev python-virtualenv```  

```virtualenv --system-site-packages -p python3```  


Install Docker and Nvidia-Docker <a name="docker"></a> 
======
### Docker CE installation  
Summarized from *https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-after-using-the-convenience-script*  

* Remove older Docker version  
```sudo apt-get remove docker docker-engine docker.io```  

* Install dependencies  
```sudo apt-get update```  
``` sudo apt-get install apt-transport-https ca-certificates curl software-properties-common```  

* Add Docker’s official GPG key  
```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```  

* Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.  
```sudo apt-key fingerprint 0EBFCD88```  
You should get:
```
    pub   4096R/0EBFCD88 2017-02-22
          Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
    uid                  Docker Release (CE deb) <docker@docker.com>
    sub   4096R/F273FCD8 2017-02-22
```  

* Set up the stable repository  
```
   sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```  

* Update and Install  
```sudo apt-get update```  
```apt-get install docker-ce```  

* Verify
```sudo docker run hello-world```  

### Nvidia-Docker installation  
Summarized from *https://github.com/NVIDIA/nvidia-docker#quick-start*  

* Remove previous versions  
```docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f```  
```sudo apt-get purge -y nvidia-docker```  

* Add the package repositories  
```
  curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
```  
```
  distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
```  
```
  curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
```  
```
  sudo apt-get update
```  

* Install nvidia-docker2 and reload the Docker daemon configuration  
```sudo apt-get install -y nvidia-docker2```  
```sudo pkill -SIGHUP dockerd```  

* Test nvidia-smi with the latest official CUDA image  
```docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi```  


Ubuntu Tweaks <a name="tweaks"></a> 
======
```sudo apt install indicator-multiload```  
