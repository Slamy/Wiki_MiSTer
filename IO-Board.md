Actual Board Revision: 3.1 (Commit: [319f0d8](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/319f0d8e7f890be3a142081aef5020b61d513411/Addons/IOBoard))

The MiSTer IO Board is an **optional** expansion board for the DE10-Nano FPGA Board. It adds the following features to the MiSTer Platform:
* VGA Connector
* 3.5mm Audio Jack
* Optical Fiber Connector (TOSLINK)
* 3x Pushbuttons
* 3x Status LEDs

All this can be either mounted directly on the IO Board or externally by connectors (e.g. case mounted)

![alt text](https://image.ibb.co/kzn1ga/Ioexample.jpg)

## Buy / Sell Spare Boards:
Since the PCBs are always ordered in batches of at least 5 Boards, most DIY users have some boards left. If you are looking for a IO board or you have some left from your last assembly, check the sale threads:
  * [Spare Boards Sale Thread (atari-forum.com)](http://www.atari-forum.com/viewtopic.php?f=33&t=32121)

## PCB Assembly

Component Overview:

| Name | Component | Package | Value | Note |
|---|---|:---:|:---:|:---:|
| C1, C2, C3, C4 | Capacitor (Ceramic) | 0805 | 1nF | - |
| C5, C6, C8 | Capacitor (Ceramic) | 2312 | 100uF | - |
| C7 | Capacitor (Tantalum) | 0805 | 1uF | - |
| C9 | Capacitor (Ceramic) | 0805 | 10uF | - |
| R1, R7, R13 | Resistor 1% 1/8W | 0805 | 500 | - |
| R2, R8, R14 | Resistor 1% 1/8W | 0805 | 1.1K | - |
| R3, R9, R15 | Resistor 1% 1/8W | 0805 | 2.2K | - |
| R4, R10, R16 | Resistor 1% 1/8W | 0805 | 4.3K | - |
| R5, R11, R17 | Resistor 1% 1/8W | 0805 | 9.1K | - |
| R6, R12, R18 | Resistor 1% 1/8W | 0805 | 18K | - |
| R19, R20 | Resistor 5% 1/8W | 0805 | 100 | - |
| R21, R22, R23 | Resistor 5% 1/8W | 0805 | 200 | - |
| R24, R25, R26, R27 | Resistor 5% 1/8W | 0805 | 560 | - |
| R28 | Resistor 5% 1/8W | 0805 | 10K | - |
| R29 | Resistor 5% 1/8W | 0805 | 1K | - |
| R30 | Resistor 5% 1/8W | 0805 | 680 | - |
| D1, D2 | General Purpose Diode | SOD80 | BAV100 | - |
| LED1 | LED Red | 3mm T/H | - | - |
| LED2 | LED Yellow | 3mm T/H | - | - |
| LED3 | LED Green | 3mm T/H | - | - |
| SW1, SW2, SW3 | Switch Tactile | | - | - |
| P1 | Female Header, Double Row, Isolation Height: 11.05mm | 2,54mm Pitch | - | - |
| P2, P3, P4, P5, P6, P7, P8, P9 | Male Pin Header, Single Row | 2.54mm Pitch | - | - |
| Q1 | Transistor NPN | SOT23 | BC847 | - |
| J1 | VGA D-Sub 15 Pos, 3 Row, Female Connector, T/H, Right Angle | - | - | - |
| J2 | Phone Jack 3.5mm, T/H, Right Angle | - | - | - |
| U1 | TOSLINK Optical Fiber Connector | - | - | Optional |

Bill of Material:
* [IO Board (v3.1)](https://octopart.com/bom-tool/Iuxmkjii) (Without TOSLINK)

Gerber Files :
* [IO Board (v2.7)](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/319f0d8e7f890be3a142081aef5020b61d513411/gerber_releases/iobrd_2.7.zip?raw=true)
* [IO Board (v3.1)](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/319f0d8e7f890be3a142081aef5020b61d513411/gerber_releases/iobrd_3.1.zip?raw=true)
