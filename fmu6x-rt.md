
요청내용
fmu-v6xrt 보드의 설정은
PX4-Autopilot-main\boards\px4\fmu-v6xrt\nuttx-config\include
폴더에 board.h 가 mcu에 대한 정보를 가지고 있음.

여기에 1G설정 정보가 기재된거 같으나
제품은 100Mbps 임.

NXP1170 EVB- 1G지원보드 설정을 보면
다르게 회로가 설정되어 있음.

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

