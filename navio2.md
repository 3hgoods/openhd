
https://github.com/ArduPilot/ardupilot/blob/master/BUILD.md

git clone --recursive https://github.com/ArduPilot/ardupilot.git
cd ardupilot

./waf configure --board navio2 
./waf copter


Build directory: /home/h1/ardupilot/build/navio2


./waf list | grep examples/
./waf list | grep 'examples'

examples/AC_PID_test 
examples/AHRS_Test 
examples/AP_Common 
examples/AP_Compass_test 
examples/AP_Declination_test 
examples/AP_Logger_AllTypes 
examples/AP_Logger_test 
examples/AP_Marvelmind_test 
examples/AP_Mission_test 
examples/AP_Motors_test 
examples/AP_Notify_test 
examples/AP_OpticalFlow_test 
examples/AP_Parachute_test 
examples/Airspeed 
examples/AnalogIn 
examples/BARO_generic 
examples/BinarySem 
examples/BusTest 
examples/CompassCalibrator_index_test 
examples/DSP_test 
examples/Derivative 
examples/File_IO 
examples/Filter 
examples/FlashTest 
examples/GPIOTest 
examples/GPS_AUTO_test 
examples/GPS_UBLOX_passthrough 
examples/Hello 
examples/ICM20789 
examples/INS_generic 
examples/LowPassFilter 
examples/LowPassFilter2p 
examples/ModuleTest 
examples/NMEA_Output 
examples/Printf 
examples/RCInput 
examples/RCInputToRCOutput 
examples/RCOutput 
examples/RCOutput2 
examples/RCProtocolDecoder 
examples/RCProtocolTest 
examples/RC_Channel 
examples/RC_UART 
examples/RFIND_test 
examples/RNG_test 
examples/RPM_generic 
examples/RTC_test 
examples/ReplayGyroFFT 
examples/RingBuffer 
examples/Scheduler_test 
examples/SlewLimiter 
examples/SmartRTL_test 
examples/Storage 
examples/StorageTest 
examples/ToshibaLED_test 
examples/TransferFunctionCheck 
examples/UART_chargen 
examples/UART_test 
examples/XPlane 
examples/eulers 
examples/expo_inverse_test 
examples/jedec_test 
examples/location 
examples/matrix_alg 
examples/onvif_test 
examples/polygon 
examples/rotations 
examples/routing 


examples/Printf 



./waf --targets examples/UART_Test --upload

------------------------------------------
./waf configure --board fmuv3
./waf build --target examples/UART_test -upload   

위의 명령어를 2단계로 분리하는 방법

1단계
./waf configure --board fmuv3
./waf build examples/UART_Test

2단계
./waf --targets examples/UART_Test --upload

-----------------------------------------------

./waf build examples/Printf 

./waf build --target examples/Printf --upload

-----------------------------------------


./waf configure --board=navio2
./waf build examples/UART_Test


./waf --targets examples/UART_Test






forlinx@ubuntu:~/ardupilot$ ./waf build --target examples/UART_test --upload



