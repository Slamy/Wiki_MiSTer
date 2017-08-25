Actual Board Revision: 3.1U (Commit: [11c4715](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/319f0d8e7f890be3a142081aef5020b61d513411/Addons/SDRAM_uni)) & 3.2 (Commit: [11c4715](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/319f0d8e7f890be3a142081aef5020b61d513411/Addons/SDRAM_rev))

The MiSTer SDRAM Board is the only **mandatory** expansion board for the DE10-Nano FPGA board. The [SDRAM is required by most cores](../SDRAM-Requirement-by-cores) of the MiSTer platform.

## Buy / Sell Spare Boards:
Since the PCBs are always ordered in batches of at least 5 Boards, most DIY users have some boards left. If you are looking for a SDRAM board or you have some left from your last assembly, check the sale threads:
  * [Spare Boards Sale Thread (atari-forum.com)](http://www.atari-forum.com/viewtopic.php?f=33&t=32121)

## SDRAM Board Types
#### SDRAM Board Universal:
![alt text](https://image.ibb.co/iz752F/31_UBoard_Comp.png)

| | Advantages | Disadvantages |
|---|:---:|:---:|
| **Vertical** | Doesn't increase horizontal dimensions. Doesn't cover and allows better cooling for FPGA chip. Doesn't block Arduino GPIO - compatible with future or custom expansions. Easy to attach/detach. | Slightly less maximum working frequency. |
| **Horizontal Outward** | Doesn't cover and allows better cooling for FPGA chip. Doesn't block Arduino GPIO - compatible with future or custom expansions. Higher maximum working frequency. | Increases horizontal dimensions. |
| **Horizontal Inward** | Doesn't increase neither horizontal nor vertical dimensions. Higher maximum working frequency. | Blocks Arduino GPIOs - incompatible with future or custom expansions (PCB v3.2 solves this issue). Covers FPGA chip and makes cooling harder. Temperature condition is quite bad. |

## Install the SDRAM Board

The SDRAM Board will be inserted into the GPIO 0 Header of the DE10-Nano Board. Three additional pins will be inserted into the Arduino header JP3

![alt text](https://image.ibb.co/cZzku5/GPIO0.jpg)

When Plugging in the SDRAM Board, make sure to support the DE10-Nano from beneath with your thumbs. Forcing in the SDRAM Board without support can bend the DE10-Nano board and permanently damage it.

![alt text](https://image.ibb.co/mYJLu5/77_F7423_E_9796_41_E6_BC61_F84005_BFE0_E7.gif)

Removing the SDRAM Board can be tricky for some GPIO connectors and just pulling won't do it sometimes. For very tight connectors, it is recommended to wiggle the SDRAM Board back and forth to remove the connectors slowly, bit-by-bit. Just pulling with force will often bend the GPIO header.

![alt text](https://image.ibb.co/hgrenQ/522_A3_D0_E_30_A6_492_D_A208_DA109_FCB9_CEE.gif)


## Do It Yourself

The following section will walk you through all steps of creating your own SDRAM Board. It describes where to order all necessary parts like PCB and components. It will also give you an overview on the equipment you need and show you how to assemble the board.

### 1. Order PCB

#### PCB Manufactor
* [PCBway](https://www.pcbway.com/setinvite.aspx?inviteid=43024)
* [EasyEDA](https://easyeda.com/)
* [OSH Park](https://oshpark.com/)

#### PCB Layout (Gerber Files)
Check the MiSTer hardware repository for the most recent PCB files: [MiSTer_Hardware](https://github.com/MiSTer-devel/Hardware_MiSTer)

* [SDRAM Board Universal (v3.1U)](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/319f0d8e7f890be3a142081aef5020b61d513411/gerber_releases/sdram_uni_3.1U.zip) --> [One-click order on PCBWay](https://www.pcbway.com/project/shareproject/MiSTer_SDRAM_board_v3_1__Universal_.html)
* [SDRAM Board Reverse (v3.2)](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/319f0d8e7f890be3a142081aef5020b61d513411/gerber_releases/sdram_rev_3.2.zip)  --> [One-click order on PCBWay](https://www.pcbway.com/project/shareproject/MiSTer_SDRAM_board_v3_2__Reversed_.html)
### 2. Order Components

#### Components (Vertical Board)

| Name | Component | Package | Value | Note |
|---|---|:---:|:---:|:---:|
| C1, C2, C3, C4, C5 | Capacitor (Tantalum) | 0805 | 0.1uF | - |
| U1 | IC SDRAM 256MBIT 166MHZ 32MB | TSOP-54 | AS4C16M16SA-6TCN | - |
| P1 | 2x20 (40 Pos.) Female Header, Double Row, Right Angle, | 2,54mm Pitch | - | - |
| P2 | 1x3 (3 Pos.) Male Pin Header, Single Row, Right Angle, Contact Length: 5.84mm (Mating), 5.84mm (Post), Insulation Height: 2.54mm| 2,54mm Pitch | - | - |


#### Components (Horizontal Board)

| Name | Component | Package | Value | Note |
|---|---|:---:|:---:|:---:|
| C1, C2, C3, C4, C5 | Capacitor (Tantalum) | 0805 | 0.1uF | - |
| U1 | IC SDRAM 256MBIT 166MHZ 32MB | TSOP-54 | AS4C16M16SA-6TCN | - |
| P1 | 2x20 (40 Pos.) Female Header, Double Row, Isolation Height: 11.05mm | 2,54mm Pitch | - | - |
| P3 | 1x3 (3 Pos.) Male Pin Header, Single Row, Straight, Contact Length: 6.1mm (Mating), 3mm (Post), Insulation Height: 2.54mm| 2,54mm Pitch | - | - |

### 3. Assemble the Board

#### Soldering Tutorial
SDRAM Board v3.1 (by [Negative Solution](https://www.youtube.com/channel/UCLHmCwunWQkMvrlgE2BJXTw)):

<a href="http://www.youtube.com/watch?feature=player_embedded&v=bq04AH7tiV0
" target="_blank"><img src="http://img.youtube.com/vi/bq04AH7tiV0/0.jpg"
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>
