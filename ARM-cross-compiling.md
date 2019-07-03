# Cross Compiling for ARM

The ARM core on the DE-10 Nano is an ARM Cortex-A9 dual core
You can grab a cross compiler for compiling ARM binaries on a 64bit intel based desktop system - eg OSX, Linux, or Windows (in the Linux subsystem)


## Using a cross compiler
`wget -c https://releases.linaro.org/components/toolchain/binaries/6.5-2018.12/arm-linux-gnueabihf/gcc-linaro-6.5.0-2018.12-x86_64_arm-linux-gnueabihf.tar.xz`

Unpack somewhere useful, eg /opt

`tar xf gcc-linaro-6.5.0-2018.12-x86_64_arm-linux-gnueabihf.tar.xz`

and add to your path.

`export CC='/opt/gcc-linaro-6.5.0-2018.12-x86_64_arm-linux-gnueabihf/bin/arm-linux-gnueabihf-gcc'`

then follow up with the usual make..

## Using Docker
Docker has a arm7 cross compiler which is easy to install on Mac or Linux (assuming you have docker installed already!)

`docker run --rm dockcross/linux-armv7 > /usr/local/sbin/dockcross-linux-armv7`

`chmod +x /usr/local/bin/dockcross-linux-arm7`

You can then cross-compile with 

`/usr/local/bin/dockcross-linux-arm7 make ./MakeFile`

or (to compile a fictitious hello.c -> hello.arm)

`/usr/local/bin/dockcross-linux-arm7 bash -c '$CC hello.c -o hello.arm'`