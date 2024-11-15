# ubuntu_notes
## Ensure gcc is installed
```sh
sudo apt install build-essential

#or some more stuff altogether
sudo apt install build-essential libssl-dev libffi-dev python-dev
```

## Python 3 stuff

Classic update before doing anythin:
```sh
sudo apt update && sudo apt upgrade
```

Python3 is already installed. Install pip:
```sh
sudo apt install python3-pip
```

Check versions:
```sh
pip3 --version
#or
pip3 -V

python3 -V
```

...and some must packages:
```sh
pip3 install numpy matplotlib pandas seaborn scikit-learn requests pillow
```

To proceed installing an environment write the following (`venv` is part of the standard Python 3 library):
```sh
sudo apt install -y python3-venv

#make a directory
mkdir environments
cd environments

#create an envinronment (it will create a directory)
python3 -m venv my_env

#to activate environment
source my_env/bin/activate

#to leave the environment
deactivate
```


Export requirements

```sh
pip freeze > requirements.txt
```

Update requirements
```sh
pip install --upgrade -r requirements.txt
```

Check dependencies integrity
```sh
pip check
```

## WSL specific
Run VS code (and install it if missing) from the current directory:
```sh
code .
```
On error see the current WSL version (2 must be selected):
```sh
wsl -l -v
```
...and update it to 2
```sh
wsl --set-version Ubuntu-22.04 2
```

## WSL Cuda

Install nvidia cuda toolkit:
```sh
sudo apt install nvidia-cuda-toolkit
```

Check cuda version:
```sh
nvcc --version
```

Example:
```console
cliff@DESKTOP-TBDVVBV:~$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Thu_Nov_18_09:45:30_PST_2021
Cuda compilation tools, release 11.5, V11.5.119
Build cuda_11.5.r11.5/compiler.30672275_0
```

Check NVIDIA driver:
```console
cliff@DESKTOP-TBDVVBV:~/cuda$ nvidia-smi
Fri Jan 12 14:51:54 2024
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 545.36                 Driver Version: 546.33       CUDA Version: 12.3     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce RTX 3060 ...    On  | 00000000:01:00.0  On |                  N/A |
| N/A   47C    P8              16W / 130W |    184MiB /  6144MiB |      5%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|  No running processes found                                                           |
+---------------------------------------------------------------------------------------+
```

Add HPC SDK (includes `nvfortran` compiler):

https://developer.nvidia.com/hpc-sdk-downloads

Instructions are the following:

```console
$ curl https://developer.download.nvidia.com/hpc-sdk/ubuntu/DEB-GPG-KEY-NVIDIA-HPC-SDK | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-hpcsdk-archive-keyring.gpg
$ echo 'deb [signed-by=/usr/share/keyrings/nvidia-hpcsdk-archive-keyring.gpg] https://developer.download.nvidia.com/hpc-sdk/ubuntu/amd64 /' | sudo tee /etc/apt/sources.list.d/nvhpc.list
$ sudo apt-get update -y
$ sudo apt-get install -y nvhpc-23-11-cuda-multi
```

Default path for HPC SDK compilers is shown below (check it after installation):

```console
cliff@DESKTOP-TBDVVBV:/opt/nvidia/hpc_sdk/Linux_x86_64/23.11/compilers/bin$ ls
compute-sanitizer  localrc-lock  nsys-ui           nvc++       nvextract  nvunzip       pgcc        pgf95      pgzip
cuda-gdb           makelocalrc   nv-nsight-cu-cli  nvcc        nvfortran  nvzip         pgcpuid     pgfortran  rcfiles
cuda-memcheck      ncu           nvaccelerror      nvcpuid     nvprepro   pgaccelerror  pgcudainit  pgprepro   tools
cuobjdump          ncu-ui        nvaccelinfo       nvcudainit  nvprof     pgaccelinfo   pgf77       pgsize
localrc            nsys          nvc               nvdecode    nvsize     pgc++         pgf90       pgunzip
```

To add it to the `PATH` variable add the following line to `~/.profile`:
```bash
PATH="/opt/nvidia/hpc_sdk/Linux_x86_64/23.11/compilers/bin:$PATH"
```
Below the full version:
```bash
NVARCH=`uname -s`_`uname -m`
NVCOMPILERS=/opt/nvidia/hpc_sdk
MANPATH="$MANPATH:$NVCOMPILERS/$NVARCH/23.11/compilers/man"
PATH="$NVCOMPILERS/$NVARCH/23.11/compilers/bin:$PATH"
MODULEPATH="$NVCOMPILERS/modulefiles"
```


And reload the `PATH` variable with the following:
```sh
source ~/.profile
```




# Mount iso (with greek paths)

```bash
genisoimage -o cd.iso -J -R -l .
```

# Update Python

Nice link:

https://cloudbytes.dev/snippets/upgrade-python-to-latest-version-on-ubuntu-linux


Add deadsnakes repository and update:

```sh
sudo apt update && sudo apt upgrade -y
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
```

Check if the version is there:
```console
cliff@DESKTOP-TBDVVBV:~$ apt list | grep python3.12

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

idle-python3.12/jammy 3.12.1-1+jammy3 all
libpython3.12-dbg/jammy 3.12.1-1+jammy3 amd64
libpython3.12-dev/jammy 3.12.1-1+jammy3 amd64
libpython3.12-minimal/jammy 3.12.1-1+jammy3 amd64
libpython3.12-stdlib/jammy 3.12.1-1+jammy3 amd64

```

Then install the desired version:

```sh
sudo apt install python3.12
sudo apt-get install python3.12-venv

sudo apt install python3.13
sudo apt install python3.13-venv
```

Check alternatives:
```sh
sudo update-alternatives --config python3
```

Add alternatives 
```sh
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 0
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.13 3

```

Fix pip

```sh
sudo apt remove --purge python3-apt
sudo apt autoclean
sido apt install python3-apt
```

Download and install pip (after fixing)

```sh
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
sudo python3.13 get-pip.py
```

Create environment

```sh
python3 -m venv keftenv
```

Activate environment
```sh
source keftenv/bin/activate
```

Deactivate environment
```sh
deactivate
```

Install requirements
```sh
pip install -r requirements.txt
```

Remove alternative
```sh
sudo update-alternatives --remove python3 /usr/bin/python3.12
```


Update pip
```sh
pip3 install --update pip
```
or (note both fields should be `pip` not `pip3` here):
```sh
python3 -m pip install --upgrade pip
```

# Install dotnet

Based on the guide of https://tecadmin.net/how-to-install-dotnet-core-on-ubuntu-22-04/

## Check current os
```sh
cat /etc/os-release
```

Download and install MS package signing key and repo:

```sh
wget -q https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
```
If everything ok install the .NET SDK
```sh
sudo apt update
sudo apt install -y dotnet-sdk-8.0
```

# Install ssh on Ubuntu

```sh
sudo apt install openssh-server
sudo systemctl enable ssh
sudo ufw allow ssh
sudo systemctl start ssh
```
# See list of recent installs

```sh
grep " install " /var/log/dpkg.log
```
