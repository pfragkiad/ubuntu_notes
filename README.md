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

Install nvidia cuda toolkit
```sh
sudo apt install nvidia-cuda-toolkit
```

# Mount iso (with greek paths)

```bash
genisoimage -o cd.iso -J -R -l .
```
