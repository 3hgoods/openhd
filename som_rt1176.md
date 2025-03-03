

phyCORE®-RT1170
https://www.phytec.com/product/phycore-rt1170/


SDK 이용
http://www.wearedev.net/?m=bbs&bid=lecture&uid=271&PHPSESSID=3abeba725ce194b03c627cf16588b620

https://donggreen.tistory.com/entry/MCU-NXP-MCUXpresso-IDE-SDK-%EC%84%A4%EC%B9%98-%EB%B0%A9%EB%B2%95



왜 free-rtos가 아닌 chibios였는가?
https://discuss.ardupilot.org/t/why-not-freertos/106060/10

cm7+cm4 사용법
https://www.nxp.com/docs/en/application-note/AN13264.pdf

http://www.wearedev.net/?m=bbs&bid=lecture&uid=271&PHPSESSID=3abeba725ce194b03c627cf16588b620

https://www.wpgdadatong.com.cn/blog/detail/46653

https://www.nxp.com/docs/en/quick-reference-guide/VMUQSG.pdf

-------------------------


mcpu=arm7tdmi

 [COLLECT_GCC_OPTIONS='-specs=nosys.specs' '-v' '-o' 'cmTC_aee7b' '-mcpu=arm7tdmi' '-mfloat-abi=soft' '-marm' '-march=armv4t']



 fmu-v6xrt


 /home/h1/PX4-Autopilot/platforms/nuttx/src/ px4io_serial.cpp

 /home/h1/PX4-Autopilot/platforms/nuttx/src/px4/nxp/rt117x/include/px4_arch/hw_description.h



---> fmu-v6xrt는 px4_io-v2_default.bin 을 사용하지 않나? 그런데 왜 extra에 있는거지??
/home/h1/PX4-Autopilot/Makefile

 px4io_update:
	@$(MAKE) --no-print-directory px4_io-v2_default
	@$(MAKE) --no-print-directory cubepilot_io-v2_default
	# px4_io-v2_default
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/ark/fmu-v6x/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/holybro/durandal-v1/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/holybro/pix32v5/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/mro/x21/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/mro/x21-777/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/px4/fmu-v2/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/px4/fmu-v3/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/px4/fmu-v4pro/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/px4/fmu-v5/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/px4/fmu-v5x/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/px4/fmu-v6x/extras/px4_io-v2_default.bin
	cp build/px4_io-v2_default/px4_io-v2_default.bin boards/px4/fmu-v6c/extras/px4_io-v2_default.bin
	# cubepilot_io-v2_default
	cp build/cubepilot_io-v2_default/cubepilot_io-v2_default.bin boards/cubepilot/cubeorange/extras/cubepilot_io-v2_default.bin
	cp build/cubepilot_io-v2_default/cubepilot_io-v2_default.bin boards/cubepilot/cubeyellow/extras/cubepilot_io-v2_default.bin
	git status
