

설명서 https://github.com/ArduPilot/ardupilot/blob/master/BUILD.md
https://stella47.tistory.com/404

-------------
기본설치
https://852completed.tistory.com/120

git clone --recursive https://github.com/ArduPilot/ardupilot.git
cd ardupilot
Tools/environment_install/install-prereqs-ubuntu.sh -y
. ~/.profile
git status
./waf distclean

----------------------------------------
예제 컴파일
https://ardupilot.org/dev/docs/learning-ardupilot-the-example-sketches.html
https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_InertialSensor/examples/INS_generic


The board target px4-v2 has been removed from ArduPilot with the removal of NuttX support and HAL_PX4.
Please use a replacement build as follows:
 px4-v2     Use Pixhawk1 build
 px4-v3     Use Pixhawk1 or CubeBlack builds
 px4-v4     Use Pixracer build
 px4-v4pro  Use DrotekP3Pro build


./waf configure --board Pixhawk1
./waf --target examples/INS_generic --upload
353736-if00: [Errno 13] Permission denied: '/dev/serial/by-id/usb-ArduPilot_fmuv3_2B0022000A51393032353736-if00'
Exception creating uploader: [Errno 13] could not open port /dev/serial/by-id/usb-ArduPilot_fmuv3_2B0022000A51393032353736-if00: [Errno 13] Permission denied: '/dev/serial/by-id/usb-ArduPilot_fmuv3_2B0022000A51393032353736-if00'
Exception creating uploader: [Errno 13] could not open port /dev/serial/by-id/usb-ArduPilot_fmuv3_2B0022000A51393032353736-if00


./waf configure --board=Pixhawk1
  160  ./waf build --target examples/INS_generic --upload
  161  ./waf distclean
  162  ./waf configure --board=fmuv3
  163  ./waf build --target examples/INS_generic --upload
  164  ./waf distclean
  165  ./waf configure --board=pixhawk-nano-v5
  166  ./waf configure --board=CUAVv5Nano
  167  ./waf build --target examples/INS_generic --upload





----------------------------------------
 sudo apt install mc
  125  mc
  126  cd ..
  127  cd libraries/AP_HAL_ChibiOS/hwdef/
  128  cp fmuv5 fmuv7
  129  cp -r fmuv5 fmuv7
  130  cd ..
  131  history
  132  ./waf distclean
  133  ./waf configure --board fmuv7
  134  cp Tools/bootloaders/fmuv5_bl.bin Tools/bootloaders/fmuv7_bl.bin
  135  ./waf configure --board fmuv7
  136  history
  137  ./waf build --target examples/INS_generic
  138  ./waf build --target copter
  139  ./waf copter
----------------------------------------


------------------

Steps to build IOMCU firmware 
인용문서 https://soil21.tistory.com/190


Clone the ArduPilot repository
Run Tools/scripts/build_iofirmware.py
Run ./waf configure --board iomcu-dshot








