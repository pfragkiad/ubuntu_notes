# ubuntu_notes
## Install pip on Ubuntu 22

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
