
uno 
https://zephyr-workbench.com/docs/tutorials/arduino-uno-r4-wifi/



pyocd 툴 설치 별도
https://blog.naver.com/chcbaram/223240810583



설치 가이드
기본 https://docs.zephyrproject.org/latest/develop/getting_started/index.html

vscode 이용 설치가이드
https://zephyr-workbench.com/docs/documentation/installation
https://zephyr-workbench.com/docs/tutorials/arduino-uno-r4-wifi/

https://engschool.tistory.com/126


https://bootlin.com/blog/getting-started-with-zephyr/

핵심원리
https://m.blog.naver.com/chcbaram/222755342935


==================
    1  wget https://apt.kitware.com/kitware-archive.sh
    2  sudo bash kitware-archive.sh
    3  sudo apt install --no-install-recommends git cmake ninja-build gperf   ccache dfu-util device-tree-compiler wget   python3-dev python3-pip python3-setuptools python3-tk python3-wheel xz-utils file   make gcc gcc-multilib g++-multilib libsdl2-dev libmagic1
    4  cmake --version
    5  python3 --version
    6  dtc --version
    7  sudo apt install python3-venv
    8  python3 -m venv ~/zephyrproject/.venv
    9  source ~/zephyrproject/.venv/bin/activate
   10  pip3 install --upgrade pip
   11  pip install west
   12  history
   13  west init ~/zephyrproject
   14  cd ~/zephyrproject
   15  west update
   16  history
   17  west zephyr-export
   18  west packages pip --install
   19  pip install -r zephyr/scripts/requirements.txt
   20  cd ~
   21  mkdir zephyr-sdk
   22  cd zephyr-sdk
   23  wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.8/zephyr-sdk-0.16.8_linux-x86_64.tar.xz
   https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.17.0/zephyr-sdk-0.17.0_linux-x86_64.tar.xz
   
   24  tar xvf zephyr-sdk-0.16.8_linux-x86_64.tar.xz
   25  cd zephyr-sdk-0.16.8/
   26  ls
   27  ./setup.sh
   28  cd ..
   29  ls
   30  cd ..
   31  cd zephyrproject/
   32  ls
   33  cd zephyr/
   34  west build -p auto -b qemu_cortex_m3 samples/synchronization
   35  west build -t run

=====================================================================

혼용할 것.
https://engschool.tistory.com/126

****
https://docs.zephyrproject.org/latest/boards/nxp/vmu_rt1170/doc/index.html

수정
현재 west build -b vmu_rt1170 samples/hello_world
수정 west build -b vmu_rt1170/mimxrt1176/cm7 samples/hello_world









-----------------------------------------------------------------------------------

west zephyr-export
Zephyr (/home/h1/zephyrproject/zephyr/share/zephyr-package/cmake)
has been added to the user package registry in:
~/.cmake/packages/Zephyr

ZephyrUnittest (/home/h1/zephyrproject/zephyr/share/zephyrunittest-package/cmake)
has been added to the user package registry in:
~/.cmake/packages/ZephyrUnittest

-----------------------------------------------------------------------------------




예제 빌드
https://github.com/LairdCP/BL65x-Zephyr-Tutorials/blob/master/docs/ubuntu.md

예제빌드
https://engschool.tistory.com/126

예제빌드 x86
https://docs.nordicsemi.com/bundle/ncs-2.5.2/page/zephyr/samples/hello_world/README.html#hello-world

예제빌드 rt1176
https://docs.nordicsemi.com/bundle/ncs-2.5.2/page/zephyr/boards/arm/vmu_rt1170/doc/index.html

west build -b vmu_rt1170 samples/hello_world

west build -p always -b <your-board-name> samples/basic/blinky


---에러 해결1
echo 'export ZEPHYR_SDK_INSTALL_DIR=~/zephyr-sdk-0.17.0' >> ~/.bashrc
source ~/.bashrc





한글 동영상강의
https://youtu.be/PDG1e65Wsz0




https://docs.nordicsemi.com/bundle/ncs-2.5.2/page/zephyr/boards/arm/vmu_rt1170/doc/index.html

The VMU RT1170 features an i.MX RT1176 dual core MCU with the Cortex-M7 core at 1 GHz and a Cortex-M4 at 400 MHz. The i.MX RT1176 MCU offers support over a wide temperature range and is qualified for consumer, industrial and automotive markets. The VMU RT1170 is the default VMU for CogniPilot’s Cerebri, a Zephyr RTOS based Autopilot.

====================
예제
https://docs.zephyrproject.org/latest/boards/st/nucleo_f103rb/doc/index.html



===
업로드ㅡ 안되는 문제 해결

   75  sudo apt install openocd
   76  west flash --runner openocd
   77  sudo west flash --runner openocd
   78  sudo usermod -a -G plugdev $USER
   79  west flash --runner openocd
   80  sudo udevadm control --reload-rules && sudo udevadm trigger
   81  west flash --runner openocd
   82  history



west build -b nucleo_f103rbc samples/hello_world 


예제2
https://slowbootkernelhacks.blogspot.com/2024/11/zephyr-rtos-programming.html


west build -b nucleo_l432kc samples/hello_world -t menuconfig

west build -b nucleo_f103rb samples/hello_world -t menuconfig
sudo minicom -D /dev/ttyACM0 -b 115200
빠져나가는 방법 컨트롤 X 하고 A키를 누른뒤 손을 뗀 후 
 키를 누릅니다

 
Minicom에서 빠져나가려면 다음 단계를 따라 주세요:
**CTRL + A**를 누릅니다.
그런 다음 X 키를 누릅니다.
"Leave without reset?" (리셋 없이 종료할까요?)라는 메시지가 나오면 **Enter**를 눌러 종료합니다.
만약 강제 종료하려면 **CTRL + A**를 누른 후 **Q**를 입력


연결된 디바이스 확인방법 >>>>>>>>>
최근 연결된 USB 장치의 정보를 확인할 수 있습니다.
dmesg | grep ttyACM

현재 연결된 USB 직렬 장치를 확인
ls /dev/ttyACM*

USB 장치 목록을 확인하여 어떤 장치가 연결되어 있는지 확인
lsusb

해당 포트의 상세 정보를 확인
udevadm info -q property -n /dev/ttyACM0


옞[3
https://docs.zephyrproject.org/latest/boards/st/nucleo_f103rb/doc/index.html

west build -b nucleo_f103rb samples/basic/blinky
   90  west flash --runner openocd





--------------


 유사1
https://nxp.gitbook.io/mr-b3rb/advanced-untested-and-rough-notes/configuring-cerebri-software-for-mr-canhubk344-without-power-measurement-capability

