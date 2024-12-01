
Raspberry PI 4S에 OpenHD Ground 설정 방법

1. 가정

   1) Raspberry PI 4S에 Raspberry PI OS(64bit) Bookworm Lite가 이미 설치되어 있다고 가정한다.
       OS는 32bit 64bit 아무거나 가능하나 Raspberry측에서 현재 64bit를 추천하고 있슴.

   2) network 사용시 접속 방법
      ssh pi@ip주소
          
            * ip주소는 공유기 등을 통해서 알아 내야한다.

   3) serial 사용시 접속 방법
      SD를 pc에 연결하여 boot directory안에 config.txt를 찾아 맨 아래줄에 아래 내용을 추가해주면 serial port 출력이 가능해진다.
      
      --- config.txt ---
              :
              :
      enable_uart=1
      
 
2. 개발환경 설치

   1) Qt 및 qtcreator 관련 설치
       sudo apt update
       sudo apt upgrade
       sudo apt install apt-transport-https mc bc git
       sudo apt install qtbase5-dev qtdeclarative5-dev qt5-qmake qtcreator libqt5gui5  qtscript5-dev qtmultimedia5-dev libqt5multimedia5-plugins qtquickcontrols2-5-dev libqt5network5 cmake build-essential
       sudo apt install qtcreator

    2) gstreamer 관련 설치 
       sudo apt install gstreamer1.0-tools
       sudo apt install libgstreamer1.0-dev      libgstreamer-plugins-base1.0-dev      libgstreamer-plugins-bad1.0-dev      gstreamer1.0-plugins-ugly      gstreamer1.0-tools      gstreamer1.0-gl      gstreamer1.0-gtk3
       sudo apt install libx264-dev libjpeg-dev
       sudo apt install gstreamer1.0-qt5
       sudo apt install gstreamer1.0-pulseaudio
       sudo apt install gstreamer1.0-gl libgstreamer1.0-dev  gstreamer1.0-plugins-good libgstreamer-plugins-base1.0-dev gstreamer1.0-plugins-base libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly  libxcb-cursor0

    3) qtcharts 설치
       위과정으로 qmake 가 설치되었으면 qmake의 version을 확인하여 같은 versiondml 화일을 가져온다.
       pi@raspberrypi:~ $ qmake -version
       QMake version 3.1
       Using Qt version 5.15.8 in /usr/lib/aarch64-linux-gnu

       pi@raspberrypi:~ $ wget https://download.qt.io/archive/qt/5.15/5.15.8/submodules/qtcharts-everywhere-opensource-src-5.15.8.tar.xz

       압축 풀고 source가 있는 Directory(qtcharts-everywhere-src-5.15.8)로 이동 후 make; sudo make install
 
       pi@raspberrypi:~ $ tar xvf qtcharts-everywhere-opensource-src-5.15.8.tar.xz 
       pi@raspberrypi:~ $ cd qtcharts-everywhere-src-5.15.8
       pi@raspberrypi:~/qtcharts-everywhere-src-5.15.8 $  qmake
       pi@raspberrypi:~/qtcharts-everywhere-src-5.15.8 $  make -j4( make 사용 약 30분이상 소용됨) 
       pi@raspberrypi:~/qtcharts-everywhere-src-5.15.8 $  sudo make install

    4) 무선랜 rtl8812au Device Driver 설치
        OpenHD 공식 git https://github.com/OpenHD에서 (주의 OpenHD관련 다른 유사한 url 도 많음)에서 rtl8812au source 를 가져온다.

        pi@raspberrypi:~ $ git clone https://github.com/OpenHD/rtl8812au

        OpenHD 공식 git에는rtl8812au 말고도 rtl88x2eu / rtl88x2cu /rtl88x2bu의 Device Driver source가 있다.
        현재 사용하는 무선랜에 맞게 가져오면 된다.

        source가 있는 Directory(rtl8812au)로 이동 후 

        pi@raspberrypi:~ $ cd rtl8812au
        pi@raspberrypi:~/rtl8812au $ ./build_install_no_kms.sh

                                          에러발생하는 su 사용안해서 권한 문제.
rmmod: ERROR: Module 88XXau_ohd is not currently loaded
insmod: ERROR: could not insert module 88XXau_ohd.ko: Unknown symbol in module


        pi@raspberrypi:~/rtl8812au $ sudo make install
        무선랜 rtl8812au가 USB에 삽입된 상태에서 재부팅후 module이 loading 되어 있으면 정상 설치된 것이다.
 
        pi@raspberrypi:~ $ lsmod | grep 88XXau_ohd 
        .............
        88XXau_ohd           2519040  0
         
3. OpenHD compile

       pi@raspberrypi:~ $ git clone --recursive https://github.com/OpenHD/OpenHD
       반드시 --recursive 옵션을 사용하여 submodules 까지 가져와야 정상 compile 된다.

git clone -b v2.6.0 --recursive https://github.com/OpenHD/OpenHD
     
       source가 있는 Directory(OpenHD)로 이동 후 
       pi@raspberrypi:~ $ cd OpenHD
       pi@raspberrypi:~/OpenHD $ sudo ./install_build_dep.sh
       pi@raspberrypi:~/OpenHD $ sudo ./package.sh

       openhd 실행화일이 생성되었는지 확인한다.

4. QOpenHD

      pi@raspberrypi:~ $ git clone https://github.com/OpenHD/mavlink-headers.git

      pi@raspberrypi:~ $ sudo cp -Rf mavlink-headers /lib/.

      pi@raspberrypi:~ $ git clone https://github.com/OpenHD/QOpenHD   

      압축 풀고 source가 있는 Directory(QOpenHD)로 이동 후 

      Qt App 화면 size를 현재 screen size인 1920x1024로 변경해야 한다.
      vi ~/QOpenHD/qml/main.qml

      pi@raspberrypi:~ $ cd QOpenHD 
      pi@raspberrypi:~/QOpenHD $ sudo ./install_build_dep.sh
      pi@raspberrypi:~/QOpenHD $ ./build_qmake.sh
 
      complile후 아래 Directory에 QOpenHD 실행화일이 생성되었는지 학인한다.
      pi@raspberrypi:~/QOpenHD $ ls -l ./build/release/QOpenHD 
      -rwxr-xr-x 1 pi pi 44688152 Sep  6 00:11 ./build/release/QOpenHD

5.  실행 방법

     1) openhd 실행
     pi@raspberrypi:~ $ sudo /home/pi/OpenHD/openhd &
     반드시 sudo 및 백그라운드( &) 로 실행해야 한다.

     - ground는 그낭 openhd를 실행하면 된다.
     - air의 경우 /boot/openhd/air.txt 화일이 존재해야 air로 동작한다.
       air.txt안에는 아무 내용이 없어도 화일 이름만 존재하면 된다.

     실행후 몇초 (약 10초 내외) 지나서 ifconfig 에 아래(-----로 되어 있는 부분)와 같이 나오면 정상동작 한 것이다.

     pi@raspberrypi:~/OpenHD $ ifconfig
     eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
             inet 192.168.0.201  netmask 255.255.255.0  broadcast 192.168.0.255
             inet6 fe80::e532:5f88:4c5d:efca  prefixlen 64  scopeid 0x20<link>
             ether d8:3a:dd:8a:0f:46  txqueuelen 1000  (Ethernet)
             RX packets 36217  bytes 2899976 (2.7 MiB)
             RX errors 0  dropped 0  overruns 0  frame 0
             TX packets 38150  bytes 29404610 (28.0 MiB)
             TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

     lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
             inet 127.0.0.1  netmask 255.0.0.0
             inet6 ::1  prefixlen 128  scopeid 0x10<host>
             loop  txqueuelen 1000  (Local Loopback)
             RX packets 266  bytes 79134 (77.2 KiB)
             RX errors 0  dropped 0  overruns 0  frame 0
             TX packets 266  bytes 79134 (77.2 KiB)
             TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

     wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 2312
-------------------------------------------------------------------------------------------------------------------------------------
             unspec FC-A3-86-64-D7-3C-3A-30-00-00-00-00-00-00-00-00  txqueuelen 1000  (UNSPEC)
-------------------------------------------------------------------------------------------------------------------------------------
             RX packets 34  bytes 0 (0.0 B)
             RX errors 0  dropped 0  overruns 0  frame 0
             TX packets 21  bytes 1149 (1.1 KiB)
             TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

     2) QOpenHD 실행
 
        pi@raspberrypi:~ $ sudo  /home/h1/QOpenHD/build/release/QOpenHD -platform eglfs


    3) 부팅시 자동실행

       (1) openhd 자동 실행
            pi@raspberrypi:~ $ sudo vi /etc/rc.local  실행후 아래 명령어를 exit 0 이전에 삽입한다.

           sudo /home/pi/OpenHD/openhd &

       (2) QOpenHD 자동 실행

           pi@raspberrypi:~ $ sudo vi /etc/xdg/lxsession/LXDE-pi/autostart  실행후 마지막 중에 아래 명령어를 삽입한다.

           suudo /home/pi/QOpenHD/build/release/QOpenHD
      



 


 
