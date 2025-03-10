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


 유사1
https://nxp.gitbook.io/mr-b3rb/advanced-untested-and-rough-notes/configuring-cerebri-software-for-mr-canhubk344-without-power-measurement-capability

