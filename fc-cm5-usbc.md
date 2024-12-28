
https://arkelectron.gitbook.io/ark-documentation/flight-controllers/ark-jetson-pab-carrier/block-diagram

외장 usb의 사용처 구별

3.0을 찾을 수 있을까?

노트북에서 px4 정보 가져오는 것처럼 usb로 연결!!

ark px4-pi
reset signal connected to Pi pin GPIO25


holybro
CM4 GPIO14 <-> FMU TXD TELEM2
CM4 GPIO15 <-> FMU RXD TELEM2
CM4 GPIO16 <-> FMU CTS TELEM2
CM4 GPIO17 <-> FMU RTS TELEM2



cm4 ----  usb mux ---- px4
                   |
                   |
                 usb

cm4 >>>>>>  usb mux  >>>>>     <<<< usb mux <<<< px4
 
                                    >>>>>    <<<< 
                   				|
				                |
				              usb 

Pixhawk 6X talks to CM4 using Telem2 (/dev/ttyS4).

밧데리 H CAN



minicom -b 115200 -D /dev/ttyUSB0
console=ttyAMA0,115200
