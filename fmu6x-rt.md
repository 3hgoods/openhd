
ardupilot 포팅방법
https://forum.chibios.org/viewtopic.php?t=4463

예시
https://github.com/ArduPilot/ardupilot/blob/master/libraries/AP_HAL_ChibiOS/hwdef/fmuv3/hwdef.dat
여기 힌트  MCU STM32F4xx STM32F427xx

접근-->  https://github.com/ArduPilot/ardupilot/blob/master/libraries/AP_HAL_ChibiOS/hwdef/scripts/STM32F427xx.py
여기힌트 
build = {
    "CHIBIOS_STARTUP_MK"  : "os/common/startup/ARMCMx/compilers/GCC/mk/startup_stm32f4xx.mk",
    "CHIBIOS_PLATFORM_MK" : "os/hal/ports/STM32/STM32F4xx/platform.mk

접근-->  https://github.com/ChibiOS/ChibiOS/blob/master/os/common/startup/ARMCMx/compilers/GCC/mk/startup_stm32f4xx.mk
STARTUPSRC = $(CHIBIOS)/os/common/startup/ARMCMx/compilers/GCC/crt1.c
          
STARTUPASM = $(CHIBIOS)/os/common/startup/ARMCMx/compilers/GCC/crt0_v7m.S \
             $(CHIBIOS)/os/common/startup/ARMCMx/compilers/GCC/vectors.S

STARTUPINC = $(CHIBIOS)/os/common/portability/GCC \
             $(CHIBIOS)/os/common/startup/ARMCMx/compilers/GCC \
             $(CHIBIOS)/os/common/startup/ARMCMx/devices/STM32F4xx \
             $(CHIBIOS)/os/common/ext/ARM/CMSIS/Core/Include \
             $(CHIBIOS)/os/common/ext/ST/STM32F4xx

여기힌트 컴파일로 확인하여 매칭하는 스크립트 완성 필요.!!





새로운 보드 컴파일

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





이 mcu의 최종활용방법은 

---------\RT1176 M7 에 M4를 보조로 사용하는 방법 예시 알려 줘.
RT1176은 Heterogeneous Multicore Processing (HMP) 구조로, M7과 M4가 독립적인 코드 실행이 가능하지만, Shared Memory (공유 메모리)와 Messaging Unit (MU) 를 통해 서로 통신

M7 메인, M4 보조 프로세서 활용 예시
1. 전형적인 활용 방식
✅ M7 (메인) → 복잡한 연산, UI, 네트워크, 고속 제어
✅ M4 (보조) → 센서 데이터 처리, 저전력 작업, 실시간 제어 보조

2. 구현 방법 (기본 흐름)
M7이 먼저 부팅되며, M4의 실행을 제어함.
M7이 M4의 코드를 Tightly Coupled Memory (TCM) 또는 OCRAM 에 로드하고 실행 명령을 보냄.
M7과 M4가 Messaging Unit (MU) 또는 Shared Memory 를 통해 데이터를 교환함.
M7이 주요 연산을 수행하고, M4는 센서 데이터 전처리나 주기적인 작업을 담당함.



------------두 cpu간 연결
https://www.nxp.com.cn/docs/zh/training-reference-material/TIP-IMRT-MCU-APPLICATION-1.pdf

https://github.com/nxp-mcuxpresso/rpmsg-lite

✅ 간단한 메시지 전송 → MU (Messaging Unit) 활용
✅ 고속 데이터 전송 → IPC (Inter-Processor Communication) 활용
✅ 고급 메시지 시스템 → RPMsg-Lite 활용


NXP-MR-VMU-RT1176 보드설명
- https://nxp.gitbook.io/vmu-rt1176/production-v1-carrier-board-connectors
- 
https://agamrobotics.gitbook.io/docs/autopilots-flight-controller/quickstart/technical-specification
- https://nxp.gitbook.io/vmu-rt1176/examples/testing-can3-in-px4
- 

NXP-MR-VMU-RT1176 보드 회로도
 - https://github.com/NXPHoverGames/NXP-FMUMRT


   NXP RT1176 zephyr
   https://docs.nordicsemi.com/bundle/ncs-2.5.2/page/zephyr/boards/arm/vmu_rt1170/doc/index.html
   

NXP-RT1176 보드 회로도
 - https://www.nxp.com/design/design-center/development-boards-and-designs/i-mx-evaluation-and-development-boards/i-mx-rt1170-evaluation-kit:MIMXRT1170-EVKB



두 회로 비교할때 1G를 사용하기 위해 SCH55139 (레펀런스1G) 측처엄 색깔 치한 부분이 추가되어야 하고, NXP Carrier 기존 FC에서는  UART1_DEBUG와  UART4_TELEM를 죽이고 적당한 것으로 옮겨주어야 합니다.



https://www.altium.com/altium-designer-viewer


-------------------------------------------------
요청내용
fmu-v6xrt 보드의 설정은
PX4-Autopilot-main\boards\px4\fmu-v6xrt\nuttx-config\include
폴더에 board.h 가 mcu에 대한 정보를 가지고 있음.

여기에 1G설정 정보가 기재된거 같으나
제품은 100Mbps 임.

NXP1170 EVB- 1G지원보드 설정을 보면
다르게 회로가 설정되어 있음.
https://www.nxp.com/design/design-center/development-boards-and-designs/i-mx-evaluation-and-development-boards/i-mx-rt1170-evaluation-kit:MIMXRT1170-EVKB

NXP1170 EVB- 1G지원보드 설정을 그대로 적용하고
기존 UART로 자리잡던 것은 다른 핀으로 옮겨갈라고 하는데
설정값 셋팅을 확인해 주셨으면 합니다.

SW 정보
https://github.com/nxp-appcodehub/ap-ml-person-detector

https://www.nxp.com/design/design-center/software/embedded-software/application-software-packs/application-software-pack-ml-person-detector:APPSWPACK-MLPD#downloads

https://github.com/nxp-appcodehub/dm-nafe_rt1170

https://github.com/nxp-appcodehub/dm-rt1170evkb-full-appliance

rtl sw guide
https://mcuxpresso.nxp.com/appcodehub#step1



1G 이더넷을 사용하기 위한 컴파일 변경사항.

펌워에
PX4-Autopilot-main\boards\px4\fmu-v6xrt\nuttx-config\include
폴더에 board.h 가 mcu에 대한 정보를 가지고 있음.
여기에 1G설정 정보가 있느나 

/* ETH Disambiguation *******************************************************/

// This is the ENET_1G interface.

/* Dshot Disambiguation *******************************************************/

#define IOMUX_DSHOT_DEFAULT             (IOMUX_DRIVE_HIGHSTRENGTH | IOMUX_SLEW_FAST)

// Compile time selection
#if defined(CONFIG_ETH0_PHY_TJA1103)
#  define BOARD_PHY_ADDR (18)
#endif
#if defined(CONFIG_ETH0_PHY_LAN8742A)
#  define BOARD_PHY_ADDR (0)
#endif

/* Run time selection see mii.h */

#define BOARD_ETH0_PHY_LIST \
	{                                   \
		"LAN8742A",                      \
		MII_PHYID1_LAN8742A,             \
		MII_PHYID2_LAN8742A,             \
		MII_LAN8740_SCSR,                \
		0,                               \
		0xffff,                          \
		MII_LAN8720_SPSCR_10MBPS,        \
		MII_LAN8720_SPSCR_100MBPS,       \
		MII_LAN8720_SPSCR_DUPLEX,        \
		22,                              \
	},                                  \
	{                                   \
		"TJA1103",                       \
		MII_PHYID1_TJA1103,              \
		MII_PHYID2_TJA1103,              \
		0xffff,                          \
		18,                              \
		0xffff,                          \
		0,                               \
		MII_LAN8720_SPSCR_100MBPS,       \
		MII_LAN8720_SPSCR_DUPLEX,        \
		45,                              \
	},                                  \


#define GPIO_ENET2_TX_DATA00  (GPIO_ENET_1G_TX_DATA0_1|IOMUX_ENET_DATA_DEFAULT)  /* GPIO_DISP_B1_09 */
#define GPIO_ENET2_TX_DATA01  (GPIO_ENET_1G_TX_DATA1_1|IOMUX_ENET_DATA_DEFAULT)  /* GPIO_DISP_B1_08 */
#define GPIO_ENET2_RX_DATA00  (GPIO_ENET_1G_RX_DATA0_2|IOMUX_ENET_DATA_DEFAULT)  /* GPIO_EMC_B2_15  */
#define GPIO_ENET2_RX_DATA01  (GPIO_ENET_1G_RX_DATA1_2|IOMUX_ENET_DATA_DEFAULT)  /* GPIO_EMC_B2_16  */
#define GPIO_ENET2_MDIO       (GPIO_ENET_1G_MDIO_1|IOMUX_ENET_MDIO_DEFAULT)      /* GPIO_EMC_B2_20  */
#define GPIO_ENET2_MDC        (GPIO_ENET_1G_MDC_1|IOMUX_ENET_MDC_DEFAULT)        /* GPIO_EMC_B2_19  */
#define GPIO_ENET2_RX_EN      (GPIO_ENET_1G_RX_EN_1|IOMUX_ENET_EN_DEFAULT)       /* GPIO_DISP_B1_00 */
#define GPIO_ENET2_RX_ER      (GPIO_ENET_RX_ER_1|IOMUX_ENET_RXERR_DEFAULT)       /* GPIO_DISP_B1_01 */
#define GPIO_ENET2_TX_CLK     (GPIO_ENET_1G_REF_CLK_1|IOMUX_ENET_TX_CLK_DEFAULT) /* GPIO_DISP_B1_11 */
#define GPIO_ENET2_TX_EN      (GPIO_ENET_1G_TX_EN_1|IOMUX_ENET_EN_DEFAULT)       /* GPIO_DISP_B1_10 */

