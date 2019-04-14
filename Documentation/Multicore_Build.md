# COMPILING MULTICORE CODE

You can compile on both Windows or linux the makefile should be compatible to either.
>
I don't use linux but have many users who do who quickly tell me of errors (usually upper/lowercase linux is sensitive too). you will need to search out how to baremetal compile.

For windows users you will need an cross compiler and a make executable
>
<b>COMPILER:</b> https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads
>
<b>GNUMake:</b> http://gnuwin32.sourceforge.net/packages/make.htm
Select the package without guille and place on your comamnd line path
>
# THE MAKE COMMANDS
>
Make Pi2  ... Compiles ARM7 AARCH32 bit code which will run on Pi2, Pi3
>
Make Pi3  ... Compiles ARM8 AARCH32 bit code which will run only on Pi3
>
Make Pi3-64  ... Compiles ARM8 AARCH64 bit code which will run only on Pi3
>
Make clean ... Cleans up all intermediate files
>
If you wish to just try any sample a pre-compiled version is provided in the "diskimg" directory of each sample. Simply take a formatted SD card and place the files in that directory onto the root directory of the SD Card place in Pi and turn on. 
