# ubuntu_notes
## Install pip on Ubuntu 22

Classic update before doing anythin:
```bash
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
