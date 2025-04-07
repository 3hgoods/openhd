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


