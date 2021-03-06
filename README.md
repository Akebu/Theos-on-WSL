# Theos-on-WSL
Install theos in Windows Subsystem for Linux

## Requirements
First we need somes utilities :
```
sudo apt-get install build-essential
```
## To SSH over USB
* Get the latest Windows build of iFunBox and install it.
* Click on "My Device", "ToolBox", then "USB Tunnel."
* New USB Tunnel at Port : 22

## Installing Theos
#### Download the latest version of Theos :
This code will install theos in /opt/
```
cd /opt/
sudo git clone --recursive git://github.com/theos/theos.git
```

#### Download the Linux toolchain :
```
cd /opt/theos/toolchain
sudo wget https://developer.angelxwind.net/Linux/ios-toolchain_clang%2bllvm%2bld64_2016-02-03_linux_x86_64.zip -O LinuxToolchain.zip
sudo unzip LinuxToolchain.zip && sudo rm -rf LinuxToolchain.zip
```

#### Download iOS 9.0 SDK
```
cd /opt/theos/sdks
sudo wget https://sdks.website/dl/iPhoneOS9.0.sdk.tbz2 -O iOS9.sdk.tbz2
sudo tar xvjf iOS9.sdk.tbz2 && sudo rm -rf iOS9.sdk.tbz2
```

#### Add Theos environment variables to your  ~/.bashrc
```
echo export "THEOS=/opt/theos" >> ~/.bashrc
echo export "PATH=$THEOS/bin:\$PATH" >> ~/.bashrc
echo export "THEOS_DEVICE_IP=localhost THEOS_DEVICE_PORT=22" >> ~/.bashrc
echo "umask 0022" >> ~/.bashrc
source ~/.bashrc
```
## Workaround for fakeroot
On version 15063.296, fakeroot doesn't work and return this error :
```
Tony@DESKTOP-H7870G9:~$ fakeroot whoami
fakeroot, while creating message channels: Function not implemented
This may be due to a lack of SYSV IPC support.
fakeroot: error while starting the `faked' daemon.
kill : utilisation : kill [-s sigspec | -n signum | -sigspec] pid | jobspec ... ou kill -l [sigspec]
```

Instead you can use  ```fakeroot-tcp```, so we need to replace a line in /opt/theos/makefiles/package/deb.mk
```
sudo sed -i 's/\$(FAKEROOT) -r/fakeroot-tcp/g'  /opt/theos/makefiles/package/deb.mk
```
## Enjoy!
![alt text](https://akebu.github.io/cydia/wsl_working.PNG)
