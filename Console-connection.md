The DE10-nano board has console port. The console allows you to login into Linux without a network connection and also provides some debug/info which sometimes useful to track the problems.

Refer to the **UART-to-USB (USB Mini-B)** connector on the board right side in the picture below:

![UART port location](http://www.terasic.com.tw/attachment/archive/1046/image/layout_top.jpg)

## How to connect
Connect the DE10-nano board to a PC using the **UART-to-USB (USB mini type B)** connector next to micro-USB. The PC will recognize it as virtual COM port. Use any console application to connect to this COM port. I recommend [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

Verify that COM port settings are correct:
* Speed (baud rate) - 115200 bits per second
* Data bits - 8
* Stop bits - 1
* Parity - none
* Flow control - none

## U-Boot command prompt
To interrupt u-boot and get into the u-boot command prompt once connected to the DE10-Nano, hold 'ESC' on the PC and then power on or reboot the Nano (using the reset button). Startup should be interrupted and you should see a '=>' prompt. Here you can edit the kernel boot options etc.