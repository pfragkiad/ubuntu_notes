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


# Mount iso (with greek paths)

```bash
genisoimage -o cd.iso -J -R -l .
```
