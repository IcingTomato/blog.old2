---
layout: post
title: "Let's Play Quark Linux Board - Episode 2: What is GPIO?"
description: "Quark Linux Board GPIO Tutorial"
comments: false
keywords: "Quark, Linux"
---

# GPIO Layout (English version)

> Port bank A

| Port | Ball | Type | MUX 2 | MUX 3 | MUX 4 | MUX 5 | MUX 6 | MUX 7 |
| :-----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| PA00 | D11 | I/O | UART2_TX | JTAG_MS | -- | -- | PA_EINT0 | -- |
| PA01 | D5 | I/O | UART2_RX | JTAG_CK | -- | -- | PA_EINT1 | -- |
| PA02 | D6 | I/O | UART2_RTS | JTAG_DO | -- | -- | PA_EINT2 | -- |
| PA03 | E13 | I/O | UART2_CTS | JTAG_MS | -- | -- | PA_EINT3 | -- |
| PA04 | F5 | I/O | UART0_TX | -- | -- | -- | PA_EINT4 | -- |
| PA05 | H6 | I/O | UART0_RX | PWM0 | -- | -- | PA_EINT5 | -- |
| PA06 | E14 | I/O | SIM_PWREN | PWM1 | -- | -- | PA_EINT6 | -- |
| PA07 | D8 | I/O | SIM_CLK | -- | -- | -- | PA_EINT7 | -- |
| PA08 | F13 | I/O | SIM_DATA | -- | -- | -- | PA_EINT8 | -- |
| PA09 | D13 | I/O | SIM_RST | -- | -- | -- | PA_EINT9 | -- |
| PA10 | E11 | I/O | SIM_DET | -- | -- | -- | PA_EINT10 | -- |
| PA11 | F11 | I/O | TWI TWI0_SCK | DI_TX | -- | -- | PA_EINT11 | -- |
| PA12 | C13 | I/O | TWI TWI0_SDA | DI_RX | -- | -- | PA_EINT12 | -- |
| PA13 | E15 | I/O | SPI1_CS | UART3_TX | -- | -- | PA_EINT13 | -- |
| PA14 | G12 | I/O | SPI1_CLK | UART3_RX | -- | -- | PA_EINT14 | -- |
| PA15 | F14 | I/O | SPI1_MOSI | UART3_RTS | -- | -- | PA_EINT15 | -- |
| PA16 | D15 | I/O | SPI1_MISO | UART3_CTS | -- | -- | PA_EINT16 | -- |
| PA17 | C14 | I/O | OWA_OUT | -- | -- | -- | PA_EINT17 | -- |
| PA18 | B13 | I/O | PCM0_SYNC | TWI TWI1_SCK | -- | -- | PA_EINT18 | -- |
| PA19 | B14 | I/O | PCM0_CLK | TWI TWI1_SDA | -- | -- | PA_EINT19 | -- |
| PA20 | A13 | I/O | PCM0_DOUT | SIM_VPPEN | -- | -- | PA_EINT20 | -- |
| PA21 | A14 | I/O | PCM0_DIN | SIM_VPPPP | -- | -- | PA_EINT21 | -- |

> Port bank C

| Port | Ball | Type | MUX 2 | MUX 3 | MUX 4 | MUX 5 | MUX 6 | MUX 7 |
| :-----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| PC00 | C15 | I/O | NAND_WE# | SPI0_MOSI | -- | -- | -- | -- |
| PC01 | C16 | I/O | NALE | SPI0_MISO | -- | -- | -- | -- |
| PC02 | B16 | I/O | NCLE | SPI0_CLK | -- | -- | -- | -- |
| PC03 | B15 | I/O | NCE1 | SPI0_CS | -- | -- | -- | -- |
| PC04 | F16 | I/O | NCE0 | -- | --	| -- | -- | -- |
| PC05 | A17 | I/O | NRE# | SDC2_CLK | --	| -- | -- | -- |
| PC06 | E16 | I/O | NRB0 | SDC2_CMD | --	| -- | -- | -- |
| PC07 | A16 | I/O | NRB1 | -- | --	| -- | -- | -- |
| PC08 | B18 | I/O | NDQ0 | SDC2_D0 | -- | -- | -- | -- |
| PC09 | C17 | I/O | NDQ1 | SDC2_D1 | -- | -- | -- | -- |
| PC10 | D17 | I/O | NDQ2 | SDC2_D2 | -- | -- | -- | -- |
| PC11 | C18 | I/O | NDQ3 | SDC2_D3	| -- | -- | -- | -- |
| PC12 | B17 | I/O | NDQ4 | SDC2_D4	| -- | -- | -- | -- |
| PC13 | B19 | I/O | NDQ5 | SDC2_D5	| -- | -- | -- | -- |
| PC14 | F17 | I/O | NDQ6 | SDC2_D6	| -- | -- | -- | -- |
| PC15 | C19 | I/O | NDQ7 | SDC2_D7	| -- | -- | -- | -- |
| PC16 | H16 | I/O | NDQS | SDC2_RST | -- | -- | -- | -- |

> Port bank D

| Port | Ball | Type | MUX 2 | MUX 3 | MUX 4 | MUX 5 | MUX 6 | MUX 7 |
| :-----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| PD00 | C21 | I/O | RGMII_RXD3/MII_RXD3/RMII_NULL | -- | -- | -- | -- | -- |
| PD01 | H17 | I/O | RGMII_RXD2/MII_RXD2/RMII_NULL | -- | -- | -- | -- | -- |
| PD02 | B20 | I/O | RGMII_RXD1/MII_RXD1/RMII_RXD1 | -- | -- | -- | -- | -- |
| PD03 | H18 | I/O | RGMII_RXD0/MII_RXD0/RMII_RXD0 | -- | -- | -- | -- | -- |
| PD04 | A20 | I/O | RGMII_RXCK/MII_RXCK/RMII_NULL | -- | -- | -- | -- | -- |
| PD05 | F19 | I/O | RGMII_RXCTL/MII_RXDV/RMII_CRS_DV | -- | -- | -- | -- | -- |
| PD06 | B21 | I/O | RGMII_NULL/MII_RXERR/RMII_RXER | -- | -- | -- | -- | -- |
| PD07 | E18 | I/O | RGMII_TXD3/MII_TXD3/RMII_NULL | -- | -- | -- | -- | -- |
| PD08 | E20 | I/O | RGMII_TXD2/MII_TXD2/RMII_NULL | -- | -- | -- | -- | -- |
| PD09 | F21 | I/O | RGMII_TXD1/MII_TXD1/RMII_TXD1 | -- | -- | -- | -- | -- |
| PD10 | H19 | I/O | RGMII_TXD0/MII_TXD0/RMII_TXD0 | -- | -- | -- | -- | -- |
| PD11 | F20 | I/O | RGMII_NULL/MII_CRS/RMII_NULL | -- | -- | -- | -- | -- |
| PD12 | E19 | I/O | RGMII_TXCK/MII_TXCK/RMII_TXCK | -- | -- | -- | -- | -- |
| PD13 | K17 | I/O | RGMII_TXCTL/MII_TXEN/RMII_TXEN | -- | -- | -- | -- | -- |
| PD14 | L17 | I/O | RGMII_NULL/MII_TXERR/RMII_NULL | -- | -- | -- | -- | -- |
| PD15 | K18 | I/O | RGMII_CLKIN/MII_COL/RMII_NULL | -- | -- | -- | -- | -- |
| PD16 | L18 | I/O | MDC | -- | res  erved | -- | -- | -- |
| PD17 | L19 | I/O | MDIO | -- | res erved | -- | -- | -- |

> Port bank E

| Port | Ball | Type | MUX 2 | MUX 3 | MUX 4 | MUX 5 | MUX 6 | MUX 7 |
| :-----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| PE00 | B10 | I/O | CSI_PCLK | TS_CLK | -- | -- | -- | -- |
| PE01 | A10 | I/O | CSI_MCLK | TS_ERR | -- | -- | -- | -- |
| PE02 | B11 | I/O | CSI_HSYNC | TS_SYNC | -- | -- | -- | -- |
| PE03 | C10 | I/O | CSI_VSYNC | TS_DVLD | -- | -- | -- | -- |
| PE04 | C9 | I/O | CSI_D0 | TS_D0 | -- | -- | -- | -- |
| PE05 | E10 | I/O | CSI_D1 | TS_D1 | -- | -- | -- | -- |
| PE06 | D10 | I/O | CSI_D2 | TS_D2 | -- | -- | -- | -- |
| PE07 | C8 | I/O | CSI_D3 | TS_D3 | -- | -- | -- | -- |
| PE08 | C11 | I/O | CSI_D4 | TS_D4 | -- | -- | -- | -- |
| PE09 | C12 | I/O | CSI_D5 | TS_D5 | -- | -- | -- | -- |
| PE10 | E8 | I/O | CSI_D6 | TS_D6 | -- | -- | -- | -- |
| PE11 | A11 | I/O | CSI_D7 | TS_D7 | -- | -- | -- | -- |
| PE12 | B12 | I/O | CSI_SCK | TWI2_SCK | -- | -- | -- | -- |
| PE13 | C7 | I/O | CSI_SDA | TWI2_SDA | -- | -- | -- | -- |
| PE14 | C6 | I/O | -- | -- | -- | -- | -- | -- |
| PE15 | C5 | I/O | -- | -- | -- | -- | -- | -- |

> Port bank F

| Port | Ball | Type | MUX 2 | MUX 3 | MUX 4 | MUX 5 | MUX 6 | MUX 7 |
| :-----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| PF00 | D19 | I/O | SDC0_D1 | JTAG_MS | -- | -- | -- | -- |
| PF01 | A19 | I/O | SDC0_D0 | JTAG_DI | -- | -- | -- | -- |
| PF02 | D20 | I/O | SDC0_CLK | UART0_TX | -- | -- | -- | -- |
| PF03 | F18 | I/O | SDC0_CMD | JTAG_DO | -- | -- | -- | -- |
| PF04 | E21 | I/O | SDC0_D3 | UART0_RX | -- | -- | -- | -- |
| PF05 | C20 | I/O | SDC0_D2 | JTAG_CK | -- | -- | -- | -- |
| PF06 | G18 | I/O | SDC0_DET | -- | -- | -- | -- | -- |

> Port bank G

| Port | Ball | Type | MUX 2 | MUX 3 | MUX 4 | MUX 5 | MUX 6 | MUX 7 |
| :-----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| PG00 | J3 | I/O | SDC1_CLK | -- | -- | -- | PG_EINT0 | -- |
| PG01 | L2 | I/O | SDC1_CMD | -- | -- | -- | PG_EINT1 | -- |
| PG02 | H4 | I/O | SDC1_D0 | -- | -- | -- | PG_EINT2 | -- |
| PG03 | F3 | I/O | SDC1_D1 | -- | -- | -- | PG_EINT3 | -- |
| PG04 | C2 | I/O | SDC1_D2 | -- | -- | -- | PG_EINT4 | -- |
| PG05 | C1 | I/O | SDC1_D3 | -- | -- | -- | PG_EINT5 | -- |
| PG06 | G4 | I/O | UART1_TX | -- | -- | -- | PG_EINT6 | -- |
| PG07 | D3 | I/O | UART1_RX | -- | -- | -- | PG_EINT7 | -- |
| PG08 | C3 | I/O | UART1_RTS | -- | -- | -- | PG_EINT8 | -- |
| PG09 | E3 | I/O | UART1_CTS | -- | -- | -- | PG_EINT9 | -- |
| PG10 | M3 | I/O | PCM1_SYNC | -- | -- | -- | PG_EINT10 | -- |
| PG11 | D2 | I/O | PCM1_CLK | -- | -- | -- | PG_EINT11 | -- |
| PG12 | D1 | I/O | PCM1_DOUT | -- | -- | -- | PG_EINT12 | -- |
| PG13 | B1 | I/O | PCM1_DIN | -- | -- | -- | PG_EINT13 | -- |

> Port bank L

| Port | Ball | Type | MUX 2 | MUX 3 | MUX 4 | MUX 5 | MUX 6 | MUX 7 |
| :-----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| PL00 | N1 | I/O | S_TWI_SCK | -- | -- | -- | S_PL_EINT0 | -- |
| PL01 | M1 | I/O | S_TWI_SDA | -- | -- | -- | S_PL_EINT1 | -- |
| PL02 | P2 | I/O | S_UART_TX | -- | -- | -- | S_PL_EINT2 | -- |
| PL03 | R1 | I/O | S_UART_RX | -- | -- | -- | S_PL_EINT3 | -- |
| PL04 | N2 | I/O | S_JTAG_MS | -- | -- | -- | S_PL_EINT4 | -- |
| PL05 | R2 | I/O | S_JTAG_CK | -- | -- | -- | S_PL_EINT5 | -- |
| PL06 | T4 | I/O | S_JTAG_DO | -- | -- | -- | S_PL_EINT6 | -- |
| PL07 | T3 | I/O | S_JTAG_DI | -- | -- | -- | S_PL_EINT7 | -- |
| PL08 | T2 | I/O | -- | -- | -- | -- | S_PL_EINT8 | -- |
| PL09 | M6 | I/O | -- | -- | -- | -- | S_PL_EINT9 | -- |
| PL10 | V2 | I/O | S_PWM | -- | -- | -- | S_PL_EINT10 | -- |
| PL11 | U2 | I/O | S_CIR_RX | -- | -- | -- | S_PL_EINT12 | -- |

# 推算方法

## linux-3.4-sunxi源码推算

[gpio.h(可能加载不出来)](https://raw.githubusercontent.com/allwinner-zh/linux-3.4-sunxi/master/arch/arm/mach-sunxi/include/mach/gpio.h) | [gpio.h](https://github.com/allwinner-zh/linux-3.4-sunxi/blob/master/arch/arm/mach-sunxi/include/mach/gpio.h)

```cpp
/* pin group base number name space,
 * the max pin number : 26*32=832.
 */
#define SUNXI_PINCTRL 	"sunxi-pinctrl"
#define SUNXI_BANK_SIZE 32
#define SUNXI_PA_BASE	0
#define SUNXI_PB_BASE	32
#define SUNXI_PC_BASE	64
#define SUNXI_PD_BASE	96
#define SUNXI_PE_BASE	128
#define SUNXI_PF_BASE	160
#define SUNXI_PG_BASE	192
#define SUNXI_PH_BASE	224
#define SUNXI_PI_BASE	256
#define SUNXI_PJ_BASE	288
#define SUNXI_PK_BASE	320
#define SUNXI_PL_BASE	352
#define SUNXI_PM_BASE	384
#define SUNXI_PN_BASE	416
#define SUNXI_PO_BASE	448
#define AXP_PIN_BASE	1024

#define SUNXI_PIN_NAME_MAX_LEN	8

/* sunxi gpio name space */
#define GPIOA(n)	(SUNXI_PA_BASE + (n))
#define GPIOB(n)	(SUNXI_PB_BASE + (n))
#define GPIOC(n)	(SUNXI_PC_BASE + (n))
#define GPIOD(n)	(SUNXI_PD_BASE + (n))
#define GPIOE(n)	(SUNXI_PE_BASE + (n))
#define GPIOF(n)	(SUNXI_PF_BASE + (n))
#define GPIOG(n)	(SUNXI_PG_BASE + (n))
#define GPIOH(n)	(SUNXI_PH_BASE + (n))
#define GPIOI(n)	(SUNXI_PI_BASE + (n))
#define GPIOJ(n)	(SUNXI_PJ_BASE + (n))
#define GPIOK(n)	(SUNXI_PK_BASE + (n))
#define GPIOL(n)	(SUNXI_PL_BASE + (n))
#define GPIOM(n)	(SUNXI_PM_BASE + (n))
#define GPION(n)	(SUNXI_PN_BASE + (n))
#define GPIOO(n)	(SUNXI_PO_BASE + (n))
#define GPIO_AXP(n)	(AXP_PIN_BASE  + (n))
```

从上面可以看出 ` SUNXI_P~ ` 代表后面的数字，仅需加上 `n` 就可以得到Linux GPIO的真实数字

## 终端输入 cat /sys/kernel/debug/gpio

![](http://panzhifei.fun/img/2021/02/01/01/gpio.jpg)

## 终端输入 cat /sys/kernel/debug/pinctrl/pinctrl-maps

```shell
$ root@Elaina:/sys/class/gpio# cat /sys/kernel/debug/pinctrl/pinctrl-maps
Pinctrl maps:
device 1c28000.serial
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA4
function uart0

device 1c28000.serial
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA5
function uart0

device 1c28400.serial
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PG6
function uart1

device 1c28400.serial
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PG7
function uart1

device 1c28800.serial
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA0
function uart2

device 1c28800.serial
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA1
function uart2

device 1c68000.spi
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC0
function spi0

device 1c68000.spi
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC1
function spi0

device 1c68000.spi
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC2
function spi0

device 1c68000.spi
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC3
function spi0

device 1c69000.spi
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA15
function spi1

device 1c69000.spi
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA16
function spi1

device 1c69000.spi
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA14
function spi1

device 1c69000.spi
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA13
function spi1

device 1c2ac00.i2c
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA11
function i2c0

device 1c2ac00.i2c
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PA11
config 00000105

device 1c2ac00.i2c
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA12
function i2c0

device 1c2ac00.i2c
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PA12
config 00000105

device 1c2b000.i2c
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA18
function i2c1

device 1c2b000.i2c
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PA18
config 00000105

device 1c2b000.i2c
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA19
function i2c1

device 1c2b000.i2c
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PA19
config 00000105

device 1c2b400.i2c
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PE12
function i2c2

device 1c2b400.i2c
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PE12
config 00000105

device 1c2b400.i2c
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PE13
function i2c2

device 1c2b400.i2c
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PE13
config 00000105

device 1c0f000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PF0
function mmc0

device 1c0f000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PF0
config 00001e09
config 00000105

device 1c0f000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PF1
function mmc0

device 1c0f000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PF1
config 00001e09
config 00000105

device 1c0f000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PF2
function mmc0

device 1c0f000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PF2
config 00001e09
config 00000105

device 1c0f000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PF3
function mmc0

device 1c0f000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PF3
config 00001e09
config 00000105

device 1c0f000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PF4
function mmc0

device 1c0f000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PF4
config 00001e09
config 00000105

device 1c0f000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PF5
function mmc0

device 1c0f000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PF5
config 00001e09
config 00000105

device 1c0f000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PF6
function gpio_in

device 1c0f000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PF6
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC5
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC5
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC6
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC6
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC8
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC8
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC9
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC9
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC10
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC10
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC11
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC11
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC12
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC12
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC13
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC13
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC14
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC14
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC15
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC15
config 00002809
config 00000105

device 1c11000.mmc
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PC16
function mmc2

device 1c11000.mmc
state default
type CONFIGS_GROUP (4)
controlling device 1c20800.pinctrl
group PC16
config 00002809
config 00000105

device leds
state default
type MUX_GROUP (2)
controlling device 1c20800.pinctrl
group PA10
function gpio_out

device leds
state default
type MUX_GROUP (2)
controlling device 1f02c00.pinctrl
group PL10
function gpio_out

```


