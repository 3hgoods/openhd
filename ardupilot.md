

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








