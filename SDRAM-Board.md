Actual Board Revision: 3.1U (Commit: [11c4715](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/319f0d8e7f890be3a142081aef5020b61d513411/Addons/SDRAM_uni)) & 3.2 (Commit: [11c4715](https://github.com/MiSTer-devel/Hardware_MiSTer/tree/319f0d8e7f890be3a142081aef5020b61d513411/Addons/SDRAM_rev))

The MiSTer SDRAM Board is the only **mandatory** expansion board for the DE10-Nano FPGA board. The SDRAM is required by most cores of the MiSTer platform.

## Buy / Sell Spare Boards:
Since the PCBs are always ordered in batches of at least 5 Boards, most DIY users have some boards left. If you are looking for a SDRAM board or you have some left from your last assembly, check the sale threads:
  * [Spare Boards Sale Thread (atari-forum.com)](http://www.atari-forum.com/viewtopic.php?f=33&t=32121)

## SDRAM Board Types
SDRAM Board Universal:
![alt text](https://image.ibb.co/iz752F/31_UBoard_Comp.png)

### Vertical
**Advantages:**
* Doesn't increase horizontal dimensions.
* Doesn't cover and allows better cooling for FPGA chip.
* Doesn't block Arduino GPIO - compatible with future or custom expansions.
* Easy to attach/detach.

**Disadvantages:**
* Slightly less maximum working frequency.

### Horizontal outward
**Advantages:**
* Doesn't cover and allows better cooling for FPGA chip.
* Doesn't block Arduino GPIO - compatible with future or custom expansions.
* Higher maximum working frequency.

**Disadvantages:**
* Increases horizontal dimensions.

### Horizontal inward
**Advantages:**
* Doesn't increase neither horizontal nor vertical dimensions.
* Higher maximum working frequency.

**Disadvantages:**
* Blocks Arduino GPIOs - incompatible with future or custom expansions (PCB v3.2 solves this issue).
* Covers FPGA chip and makes cooling harder. Temperature condition is quite bad.


## PCB Assembly:

Components for Vertical Type (3.1U):

| Name | Component | Package | Value | Note |
|---|---|:---:|:---:|:---:|
| C1, C2, C3, C4, C5 | Capacitor (Tantalum) | 0805 | 0.1uF | - |
| U1 | IC SDRAM 256MBIT 166MHZ 32MB | TSOP-54 | AS4C16M16SA-6TCN | - |
| P1 | 2x20 (40 Pos.) Female Header, Double Row, Right Angle, | 2,54mm Pitch | - | - |
| P2 | 1x3 (3 Pos.) Male Pin Header, Single Row, Right Angle, Contact Length: 5.84mm (Mating), 5.84mm (Post), Insulation Height: 2.54mm| 2,54mm Pitch | - | - |


Components for Horizontal Type (3.1U & 3.2):

| Name | Component | Package | Value | Note |
|---|---|:---:|:---:|:---:|
| C1, C2, C3, C4, C5 | Capacitor (Tantalum) | 0805 | 0.1uF | - |
| U1 | IC SDRAM 256MBIT 166MHZ 32MB | TSOP-54 | AS4C16M16SA-6TCN | - |
| P1 | 2x20 (40 Pos.) Female Header, Double Row, Isolation Height: 11.05mm | 2,54mm Pitch | - | - |
| P3 | 1x3 (3 Pos.) Male Pin Header, Single Row, Straight, Contact Length: 6.1mm (Mating), 3mm (Post), Insulation Height: 2.54mm| 2,54mm Pitch | - | - |


## Soldering Tutorial
SDRAM Board v3.1 (by [Negative Solution](https://www.youtube.com/channel/UCLHmCwunWQkMvrlgE2BJXTw9)):

<a href="http://www.youtube.com/watch?feature=player_embedded&v=bq04AH7tiV0
" target="_blank"><img src="http://img.youtube.com/vi/bq04AH7tiV0/0.jpg"
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>
