# COMPILING MULTICORE CODE

You can compile on both Windows or linux the makefile should be compatible to either.
>
I don't use linux but my usual only error on linux is upper/lowercase to which it is sensitive. You will need to search out how to baremetal compile for the Pi (install "arm-none-eabi-gcc" or apt-get "arm-none-eabi-gcc" etc)

Windows users you will need an cross compiler and a make executable
>
#### AARCH32
>
<b>COMPILER:</b> https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads
The Win32 zip or exe file has the windows ARM AARCH32 Cross compiler
>
#### AARCH64
>
<b>COMPILER:</b> https://releases.linaro.org/components/toolchain/binaries/latest-7/aarch64-elf/
Download the i686-mingw32_aarch64-elf.tar.xz (yeah the biggest one)
>
For the windows make executable
>
<b>Make:</b> https://sourceforge.net/projects/ezwinports/files/
download "make-4.2.1-without-guile-w32-bin.zip" and set the extracted executable on the comamnd line enviroment path
>
# EDIT THE MAKEFILE
>
The make file contains paths to the compiler directories and the prefix of the executable up to the -gcc
>
An example: D:/gcc_linaro_7_4_1/bin/aarch64-elf
>
That directory needs to reflect where YOU extracted the compiler to on YOUR MACHINE
# OPEN A COMMAND LINE
>
Now change directory to the directory that holds the makefile, then use the commands below and type the bit in bold
>
# THE MAKE COMMANDS
>
**make Pi2**  ... Compiles ARM7 AARCH32 bit code which will run on Pi2, Pi3
>
**make Pi3**  ... Compiles ARM8 AARCH32 bit code which will run only on Pi3
>
**make Pi3-64**  ... Compiles ARM8 AARCH64 bit code which will run only on Pi3
>
**make clean** ... Cleans up all intermediate files
>
If you wish to just try any sample a pre-compiled version is provided in the "diskimg" directory of each sample. Simply take a formatted SD card and place the files in that directory onto the root directory of the SD Card place in Pi and turn on. 
