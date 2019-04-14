# CODE BACKGROUND
My public baremetal workings with the Raspberry Pi in Assembler and C. Much of the code here was done for and covered by articles on CodeProject.com.
>

# COMPILING REPOSITORY CODE
>
Visual Studio 2017 has recently added support for makefiles. So I finally decided to actually use a makefile system at least for the 32Bit compilation. 64 Bit compiling is still via batch file for now as I have to sort out how to support two compilers on makefiles yet.
>
I am using GNU make 3.81 on both Windows and Linux. The windows version does not require cygwin.
> 
Links for windows users
>
<b>COMPILER:</b> https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads
>
<b>GNUMake:</b> http://gnuwin32.sourceforge.net/packages/make.htm
>
<u><b>Windows users:</b></u>
>
install Visual Studio 2017, make sure you tick the C++ installation
>
Install the GCC C/C++ compiler
>
Install GNU-Make
>
Open the Visual Studio solution file in any sample directory and you are away and running.
>
<u><b>Linux users:</b></u>
>
Install your GCC compiler
>
Install The GNU-Make
>
Open a command terminal
>
Change to the sample directory
>
>
# THE MAKE COMMANDS
>
Make Pi1  ... Compiles ARM6 AARCH32 bit code which will run on Pi1, Pi2, Pi3
>
Make Pi2  ... Compiles ARM7 AARCH32 bit code which will run on Pi2, Pi3
>
Make Pi3  ... Compiles ARM8 AARCH32 bit code which will run on Pi3
>
Make Pi1clean ... Cleans up Pi1 files
>
Make Pi2clean ... Cleans up Pi3 files
>
Make Pi3clean ... Cleans up Pi3 files
>
Make Pi1Rebuild ... Will do a Pi1 clean and build
>
Make Pi2Rebuild ... Will do a Pi2 clean and build
>
Make Pi3Rebuild ... Will do a Pi3 clean and build
>
If you wish to just try any sample a pre-compiled version is provided in the "diskimg" directory of each sample. Simply take a formatted SD card and place the files in that directory onto the root directory of the SD Card place in Pi and turn on. 
>
# BACKGROUND
>
I write a lot of 64bit as well as 32Bit code on the Pi so when I am accessing 32bit registers I will always use the C/C++ standard "uin32_t" as the type. If I used "int" then in 64 bit mode my registers would suddenly go to 64bit wide which is obviously wrong and fatal. So most of my files will have #include <stdint.h> and use "unit32_t" type. The "int" width is compiler implementation defined and it is wrong to use for access to a fixed hardware register width. 
>
The files are intended as teaching excercise so the files are not broken up into library arrangements they tend to be clumped together by funcionality. I am not a great fan of using structs to represent hardware but firstly the DesignWare USB reference files were that way to start with, and Secondly it does make them easier to read as a teaching excercise. So expect it and don't complain, you are free to change it if you don't like. Where a struct represent hardware there are volatiles on every way you access the register because GCC historically had a number of bugs. Technically they don't need it but I don't have time to chase compiler bugs if they occur.
>
My assembler bootstubs called SmartStart32.S (32 bit compiling) or SmartStart64.S (64 bit compiling) autodetects Pi version and provides the base address via the variable RPi_IO_Base_Addr in both assembler and C. All hardware pointers I use simply add the offset to the detected address so there is no need to specify Pi model. I would strongly suggest you use the same technique using the detect address if you use hardware registers with something like
>
>#define PiReg ((volatile __attribute__((aligned(4))) uint32_t PiRegister*) (RPi_IO_Base_Addr + ????????))
>
rpi-SmartStart.h is the file that provides the C interface to SmartStartxx.S and adds a few Macros and 32/64 bit specific functions like global InterruptEnables and HyperThreading calls. If you need any of the functions you just #include "rpi-SmartStart.h".
