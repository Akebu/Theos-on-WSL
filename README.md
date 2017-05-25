# Theos-on-WSL
Install theos in Windows Subsystem for Linux

## Requirements
First we need somes utilities :
```
sudo apt-get install build-essential
```
To SSH over USB
* Get the latest Windows build of iFunBox and install it.
* Click on "My Device", "ToolBox", then "USB Tunnel."
* New USB Tunnel at Port : 22

## Installing Theos
Download the latest version of Theos :
```
cd /opt/
sudo git clone --recursive git://github.com/theos/theos.git
```
Download the Linux toolchain :
```
cd /opt/theos/toolchain
sudo wget https://developer.angelxwind.net/Linux/ios-toolchain_clang%2bllvm%2bld64_2016-02-03_linux_x86_64.zip -O LinuxToolchain.zip
sudo unzip LinuxToolchain.zip && sudo rm -rf LinuxToolchain.zip
```

Add Theos environment variables to your  ~/.bashrc
```
echo export "THEOS=/opt/theos" >> ~/.bashrc
echo export "PATH=$THEOS/bin:\$PATH" >> ~/.bashrc
echo export "THEOS_DEVICE_IP=localhost THEOS_DEVICE_PORT=22" >> ~/.bashrc
echo "umask 0022" >> ~/.bashrc
source ~/.bashrc
```
