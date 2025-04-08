

# compile 도구 설치

sudo apt update
sudo apt upgrade
sudo apt install build-essential flex bison dwarves libssl-dev libelf-dev cpio qemu-utils pkg-config  libncurses-dev

# kernel compile 
# uname -r 을 이용하여 kernel version이 5.15.167.4인지 확인한다.

git clone --branch linux-msft-wsl-5.15.167.4 https://github.com/microsoft/WSL2-Linux-Kernel.git
cd WSL2-Linux-Kernel

make menuconfig KCONFIG_CONFIG=Microsoft/config-wsl
# Binary Emulation -> x32 ABI for 64-bit mod 선택 안 함.
# Networking support -> Wireless -> cfg80211 관련 모두 선택,
# 특히 cfg80211 certification onus 선택
# cfg80211 wireless extensions compatibility
# .config 에 해당하는 파일은 ./Microsoft/config-wsl 이다.

make -j16 KCONFIG_CONFIG=Microsoft/config-wsl && sudo make modules_install
sudo make install

sh ./arch/x86/boot/install.sh 5.15.167.4-microsoft-standard-WSL2+ \
        arch/x86/boot/bzImage System.map "/boot"
run-parts: executing /etc/kernel/postinst.d/unattended-upgrades 5.15.167.4-microsoft-standard-WSL2+ /boot/vmlinuz-5.15.167.4-microsoft-standard-WSL2+


# Windows WSL이 구동될 때 새로 만든 kernel을 반영하도록 복사한다.
# 이미 반영된 경우 복사가 현재 동작하는 kernel이므로 복사가 안 될 수 있다.
# 이 경우 다른 이름으로 저장했다가 Windows에서 이름을 정상화하면 된다.
mkdir -p /mnt/c/WSL2
cp ./arch/x86/boot/bzImage /mnt/c/WSL2/bzImage

wsl --shutdown

# WSL 나간다
# WSL이 확실하게 shutdown되어야 하므로 확실히 하려면 PC를 재부팅하는 게 좋다.
# Windows에서 아래 파일을 수정한다.
# .wslconfig 파일이 .으로 시작하므로 탐색기에서 안 보일 수 있다.

C:\Users\<사용자 이름>\.wslconfig  
[wsl2]
kernel=C:\\WSL2\\bzImage 



작성요령
https://velog.io/@deaf52/wsl-.wslconfig%EC%9C%BC%EB%A1%9C-%EB%8F%84%EC%BB%A4-%EC%8A%A4%ED%8E%99-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0

커스텀 wsl 커널
https://velog.io/@ruby/WSL2-%EC%BB%A4%EC%8A%A4%ED%85%80-%EC%BB%A4%EB%84%90-%EB%B9%8C%EB%93%9C%ED%95%98%EA%B8%B0


# WSL을 들어간다.

# rtl8812au compile을 하기 위한 사전 조치를 한다. 
cd /lib/modules/5.15.167.4-microsoft-standard-WSL2
sudo ln -s ~/WSL2-Linux-Kernel build

# rtl8812au를 compile 한다.
cd ~
git clone https://github.com/OpenHD/rtl8812au
cd rtl8812au
./build_install_no_kms.sh

rmmod: ERROR: Module 88XXau_ohd is not currently loaded

# 아래 명령어로 88XXau_ohd.ko가 잘 loading 되었는지 확인한다.
lsmod

h1@DESKTOP-5OM6HUE:~/rtl8812au$ lsmod
Module                  Size  Used by
88XXau_ohd           2596864  0





d
$ uname -r
5.15.133.1-microsoft-standard-WSL2

lsb_release -a


$ sudo apt install linux-headers-
Display all 203 possibilities? (y or n)

h1@DESKTOP-T4ASD5D:~$ sudo apt install linux-headers-5.15.0-136-
linux-headers-5.15.0-136-generic     linux-headers-5.15.0-136-lowlatency

sudo apt install linux-headers-5.15.0-136-generic


===========20.04 기준=============================================================  
qmake -version
QMake version 3.1
Using Qt version 5.12.8 in /usr/lib/x86_64-linux-gnu
 
아래 접근근거 https://www.bilibili.com/opus/562450044998488558
wget https://download.qt.io/archive/qt/5.12/5.12.8/qt-opensource-linux-x64-5.12.8.run
chmod +x qt-opensource-linux-x64-5.12.8.run
sudo ./qt-opensource-linux-x64-5.12.8.run


   41  mkdir ~/tmp

sudo apt install linux-headers-5.15.0-136-generic
cd /usr/lib/modules/5.15.167.4-microsoft-standard-WSL2

sudo ln -s  /usr/src/linux-headers-5.15.0-136-generic build

git clone https://github.com/OpenHD/rtl8812au
cd rtl8812au
~/rtl8812au $ sudo ./build_install_no_kms.sh
~/rtl8812au $ sudo make install
        무선랜 rtl8812au가 USB에 삽입된 상태에서 재부팅후 module이 loading 되어 있으면 정상 설치된 것이다.
$ lsmod | grep 88XXau_ohd 
        .............
        88XXau_ohd           2519040  0

        

   54  make -j8

   



cd /usr/lib/modules/5.15.167.4-microsoft-standard-WSL2

sudo ln -s  /usr/src/linux-headers-5.15.0-136-generic build

cd ~/rtl8812au

make 

ls -l *.ko

88XXau_ohd.ko 생성확인.

혹은

 ./build_.install_no_kms.sh 실행


