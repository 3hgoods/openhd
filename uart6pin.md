
참조 https://blog.naver.com/PostView.nhn?blogId=emperonics&logNo=222039301356
[각 버전의 UART]

라즈베리파이 3버전이 되면서 라즈베리파이에 블루투스 기능이 추가되었는데요. 이에 따라 블루투스 기능을 가진 라즈베리파이 3, 4, zeroW 버전은 하드웨어적인 UART0(PL011)을 블루투스 통신용으로 할당해 놓았
[출처] 라즈베리파이 시리얼 통신(RaspberryPi Uart Communication)|작성자 황제곰

라즈베리파이 4에서 UART 2-5를 추가 할당해서 사용하고자 하면 dt-overlay를 수정해 주어야 하는데요. UART관련 dt-overlay는 아래 명령어를 통해 확인해 볼 수 있습니다.
[출처] 라즈베리파이 시리얼 통신(RaspberryPi Uart Communication)|작성자 황제곰

 

--------------설정
sudo nano /boot/config.txt
dtoverlay=uart3
sudo reboot
 raspi-gpio get 4-5

dtoverlay -h uart3
Params: ctsrts  


참조2 https://forums.raspberrypi.com/viewtopic.php?t=241623
. /boot/config.txt
add the following

dtoverlay=gpio-shutdown,gpio_pin=5,active_low=1,gpio_pull=up
dtparam=act_led_gpio=4
enable_uart=1
dtoverlay=miniuart_bt
dtoverlay=uart-ctsrts


참조3 https://blog.naver.com/jjong_w/222051738240






USB-to-Serial 변환기를 사용하는 경우, 포트 이름이 ttyUSB로 
표준 시리얼 포트 /dev/ttyS0, /dev/ttyS1, ... : 전통적인 RS-232 직렬 포트

Arduino와 같은 USB 장치나 일부 모뎀과 연결된 시리얼 포트는 ttyACM으

/dev/serial0는 일반적으로 시리얼 장치의 심볼릭 링크로, 시스템에서 사용 가능한 직렬 포트를 나타냅니다.

실제 장치 확인 방법:
ls -l /dev/serial0
lrwxrwxrwx 1 root root 7 Dec 17 12:34 /dev/serial0 -> /dev/ttyAMA0
Raspberry Pi: /dev/serial0는 Raspberry Pi의 기본 직렬 포트(/dev/ttyAMA0)를 가리키고, 다른 장치에서는 기본 직렬 포트가 다른 실제 장치(ttyS0, ttyUSB0 등)를 가리킬 수 있습니다.




