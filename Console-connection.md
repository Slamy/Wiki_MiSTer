DE10-nano board has console port. Console allows you to login into Linux without a network connection. Console also provides some debug/info which sometimes useful to track the problems.

## How to connect
Connect DE10-nano board to PC using mini-USB port next to micro-USB. PC will recognize it as virtual COM port. Use any console application to connect to this COM port. I recommend [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

Verify that COM port settings are correct:
* Speed (baud rate) - 115200 bits per second
* Data bits - 8
* Stop bits - 1
* Parity - none
* Flow control - none