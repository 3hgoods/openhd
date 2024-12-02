

ref https://blog.csdn.net/lida2003/article/details/130437984

-------------------------------- examples/AP_Common -------------------
1단계
./waf configure --board sitl

2단계


3단계
./waf build --target examples/AP_Common 

4단계
./build/sitl/examples/AP_Common -M quad -C

5단계 소스 살펴보기

:~/ardupilot$ vi libraries/AP_Common/examples/AP_Common/AP_Common.cpp

--------------------------------------------------------------------------

~/ardupilot$ ./build/sitl/examples/AP_Motors_test 
Starting sketch 'UNKNOWN'
Starting SITL input

~/ardupilot$ vi libraries/AP_Motors/examples/AP_Motors_test/
AP_Motors_test.cpp      nobuild.txt             wscript
MotorTestSweep.sh       run_heli_comparison.py  
h1@h1:~/ardupilot$ vi libraries/AP_Motors/examples/AP_Motors_test/AP_Motors_test.cpp 

-----------------------------------------------------------------------------------------


조금 더 읽어보기
https://ardupilot.org/dev/docs/learning-ardupilot-the-example-sketches.html    --> 픽스호크1 imu 예제되는지 확인 필요
https://docs.px4.io/v1.12/ko/flight_controller/pixhawk.html





--upload
usb 뺀후 연결하여 파일 업로드


examples/ToshibaLED_test 작동 안하는 듯함.

./waf configure --board fmuv3
./waf build --target examples/ToshibaLED_test --upload
./waf build --target examples/ICM20789 --upload
screen /dev/ttyACM0 115200
