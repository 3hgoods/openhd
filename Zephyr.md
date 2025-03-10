설치 가이드
기본 https://docs.zephyrproject.org/latest/develop/getting_started/index.html

vscode 이용 설치가이드
https://zephyr-workbench.com/docs/documentation/installation
https://zephyr-workbench.com/docs/tutorials/arduino-uno-r4-wifi/

https://engschool.tistory.com/126


https://bootlin.com/blog/getting-started-with-zephyr/




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

