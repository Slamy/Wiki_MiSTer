# Cross Compiling for ARM

The ARM core on the DE-10 Nano is an ARM Cortex-A9 dual core
You can grab a cross compiler for compiling ARM binaries on a 64bit intel based desktop system - eg OSX, Linux, or Windows (in the Linux subsystem)


## Using a cross compiler on a Linux system
`wget -c https://developer.arm.com/-/media/Files/downloads/gnu-a/10.2-2020.11/binrel/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf.tar.xz`

Unpack somewhere useful, eg /opt

`tar xf gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf.tar.xz`

and add to your path

`export PATH=$PATH:/opt/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf/bin`

optionally set CC
`export CC='/opt/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-gcc'`

then follow up with the usual make..


## Using Docker
Docker has a arm7 cross compiler which is easy to install on Mac or Linux (assuming you have docker installed already!)

`docker run --rm dockcross/linux-armv7 > /usr/local/sbin/dockcross-linux-armv7`

`chmod +x /usr/local/sbin/dockcross-linux-armv7`

You can then cross-compile with 

`/usr/local/sbin/dockcross-linux-armv7 make ./MakeFile`

or (to compile a fictitious hello.c -> hello.arm)

`/usr/local/sbin/dockcross-linux-armv7 bash -c '$CC hello.c -o hello.arm'`
 

## Using msys on Windows 10  (Note that WSL is the recommended approach for compiling under Windows)
After installing msys, download the current 10.2 binary release from the ARM site e.g.
`gcc-arm-10.2-2020.11-mingw-w64-i686-arm-none-linux-gnueabihf.tar.xz`
From this location:
https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-a/downloads

Note: the 10.3 version has isssues; please do not use that version.

Place the tar.xz file into your /opt/ folder under msys (e.g. `C:\msys64\opt\`); to decompress it, do the following *from within MSYS*:

`cd /opt`

`unxz *.xz`

`tar xvf gcc-arm-10.2-2020.11-mingw-w64-i686-arm-none-linux-gnueabihf.tar`

Then, you will probably want to rename the "gcc-arm-10.2-2020.11-mingw-w64-i686-arm-none-linux-gnueabihf" folder to something shorter, like "arm".

Then when running MSYS set your PATH variable to point to it:

`export PATH=$PATH:/opt/<folder name from above>/bin`

## Alternatives
[Another, more complicated option for big projects targeting for ARM](Native-ARMv7-Toolchain-on-x86-64)
