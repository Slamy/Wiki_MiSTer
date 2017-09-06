The following section will walk you through the steps of creating your own Mister IO Board. It describes where to order all necessary parts like PCB and components. It will also give you an overview on the equipment you need and show you how to assemble the board.

![alt text](https://image.ibb.co/gcxvEF/IO_Board_DIY.png)

### Important Note:
I/O board has an option to provide either +5V or +3.3V through VGA PIN9. It's supposed to be used in some handmade active VGA adapters/converters. Some cables and displays have PIN9 grounded which will make short circuit if P8(VGA PWR) has jumper! It's advised not to solder P8 at all, so PIN9 won't have a power and it will be safe to connect any cable/display. Use P8 only when you are absolutely sure you need the power on PIN9.

------

### 1. Order PCB

#### Approved PCB Manufactors
  * [PCBway](https://www.pcbway.com/setinvite.aspx?inviteid=43024)
  * [EasyEDA](https://easyeda.com/)
  * [JLCPCB](https://jlcpcb.com/)
  * [OSH Park](https://oshpark.com/)

#### PCB Layout (Gerber Files)
Check the MiSTer hardware repository for the most recent PCB files: [MiSTer_Hardware](https://github.com/MiSTer-devel/Hardware_MiSTer)
* [IO Board (v2.7)](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/319f0d8e7f890be3a142081aef5020b61d513411/gerber_releases/iobrd_2.7.zip?raw=true)
* [IO Board (v3.1)](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/319f0d8e7f890be3a142081aef5020b61d513411/gerber_releases/iobrd_3.1.zip?raw=true)

------

### 2. Order Components

This is a general overview of the components, including reference parts that were successfully used to assemble a MiSTer IO Board.

| Name | Component | Package | Value | Reference Parts |
|---|---|:---:|:---:|---|
| C1, C2, C3, C4 | Capacitor (Ceramic) | 0805 | 10nF | [KEMET <br> C0805C103K5RACTU](https://www.digikey.com/products/en?keywords=399-1158-1-ND) |
| C5, C6, C8 | Capacitor (Tantalum) | 2312 | 100uF | [VISHAY <br> 293D107X96R3C2TE3](https://www.digikey.com/products/en?keywords=718-1058-1-ND) |
| C7 | Capacitor (Ceramic) | 0805 | 1uF | [KEMET <br> C0805C105K4RACTU](https://www.digikey.com/products/en?keywords=399-1284-1-ND) |
| C9 | Capacitor (Ceramic) | 0805 | 10uF | [KEMET <br> C0805C106K8PACTU](https://www.digikey.com/products/en?keywords=399-4925-1-ND) |
| R1, R7, R13 | Resistor 1% 1/8W | 0805 | 500 | [YAGEO <br> RC0805FR-07510RL](https://www.digikey.com/products/en?keywords=311-510CRCT-ND) |
| R2, R8, R14 | Resistor 1% 1/8W | 0805 | 1.1K | [YAGEO <br> RC0805FR-071K1L](https://www.digikey.com/products/en?keywords=311-1.10KCRCT-ND) |
| R3, R9, R15 | Resistor 1% 1/8W | 0805 | 2.2K | [YAGEO <br> RC0805FR-072K2L](https://www.digikey.com/products/en?keywords=311-2.20KCRCT-ND) |
| R4, R10, R16 | Resistor 1% 1/8W | 0805 | 4.3K | [YAGEO <br> RC0805FR-074K3L](https://www.digikey.com/products/en?keywords=311-4.30KCRCT-ND) |
| R5, R11, R17 | Resistor 1% 1/8W | 0805 | 9.1K | [YAGEO <br> RC0805FR-079K1L](https://www.digikey.com/products/en?keywords=311-9.10KCRCT-ND) |
| R6, R12, R18 | Resistor 1% 1/8W | 0805 | 18K | [YAGEO <br> RC0805FR-0718KL](https://www.digikey.com/products/en?keywords=311-18.0KCRCT-ND) |
| R19, R20 | Resistor 5% 1/8W | 0805 | 100 | [YAGEO <br> RC0805FR-07100RL](https://www.digikey.com/products/en?keywords=311-100CRCT-ND) |
| R21, R22, R23 | Resistor 5% 1/8W | 0805 | 200 | [YAGEO <br> RC0805FR-07200RL](https://www.digikey.com/products/en?keywords=311-200CRCT-ND) |
| R24, R25, R26, R27 | Resistor 5% 1/8W | 0805 | 560 | [YAGEO <br> RC0805FR-07560RL](https://www.digikey.com/products/en?keywords=) |
| R28 | Resistor 5% 1/8W | 0805 | 10K | [YAGEO <br> RC0805FR-0710KL](https://www.digikey.com/products/en?keywords=311-560CRCT-ND) |
| R29 | Resistor 5% 1/8W | 0805 | 1K | [YAGEO <br> RC0805FR-071KL](https://www.digikey.com/products/en?keywords=311-1.00KCRCT-ND) |
| R30 | Resistor 5% 1/8W | 0805 | 680 | [YAGEO <br> RC0805FR-07680RL](https://www.digikey.com/products/en?keywords=311-680CRCT-ND) |
| D1, D2 | General Purpose Diode | SOD80 | BAV100 | [VISHAY <br> BAV100-GS08](https://www.digikey.com/products/en?keywords=BAV100-GS08CT-ND) |
| LED1 | LED Red | 3mm | - | [WURTH <br> 151031SS06000](https://www.digikey.com/products/en?keywords=732-5006-ND) |
| LED2 | LED Yellow | 3mm | - | [WURTH <br> 151031YS06000](https://www.digikey.com/products/en?keywords=732-5010-ND) |
| LED3 | LED Green | 3mm | - | [WURTH <br> 151031VS04000](https://www.digikey.com/products/en?keywords=732-5007-ND) |
| SW1, SW2, SW3 | Switch Tactile | - | - | [C&K <br> RS-282G05A3-SM RT](https://www.digikey.com/products/en?keywords=CKN10384CT-ND) |
| P1 | Female Header, Double Row, Isolation Height: 11.05mm | 2,54mm | - | [No Name (AliExpress)](https://www.aliexpress.com/item/10-Pcs-2-54mm-Pitch-2x20-Pin-40-Pin-Female-Double-Row-Long-Pin-Header-Strip/32791223993.html) |
| P2 - P9 | Male Pin Header, Single Row | 2.54mm | - | [SULLINS <br> PRPC030SAAN-RC](https://www.digikey.com/products/en?keywords=S1011EC-30-ND) |
| Q1 | Transistor NPN | SOT23 | BC847 | [ON <br> BC847BLT1G](https://www.digikey.com/products/en?keywords=BC847BLT1GOSCT-ND) |
| J1 | VGA Connector, 15 Pos, 3 Row, Female Connector, Right Angle | D-Sub | - | [Omron <br> XM4L-1542-132](https://www.digikey.com/products/en?keywords=OR1096-ND) |
| J2 | Phone Jack 3.5mm, Right Angle | - | - | [CUI <br> SJ1-3523N](https://www.digikey.com/products/en?keywords=CP1-3523N-ND) |
| U1 | TOSLINK Optical Fiber Connector | - | - | [CLIFF <br> FC684208T](http://uk.rs-online.com/web/p/fibre-optic-connectors/8051677/) |

#### Bill of Material
User approved BOMs and One-Click shopping Carts. If you have successfully build a MiSTer IO Board and used your own components, then share them with us :)
* [Octopart: IO Board (3.1)](https://octopart.com/bom-tool/Iuxmkjii) (Missing Parts: P1, U1)
* [Digikey: IO Board (3.1)](http://www.digikey.de/short/qcj8tf) (Missing Parts: P1, U1)

#### Example Order
IO Board v3.1:
* [Digikey](http://www.digikey.de/short/qcj8tf)
* [AliExpress](https://www.aliexpress.com/item/10-Pcs-2-54mm-Pitch-2x20-Pin-40-Pin-Female-Double-Row-Long-Pin-Header-Strip/32791223993.html)
* [RS Online](http://uk.rs-online.com/web/p/fibre-optic-connectors/8051677/)
