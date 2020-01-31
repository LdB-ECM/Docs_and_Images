# COMPILING AARCH64 CODE

You can compile on both Windows or linux the makefile should be compatible to either.
>I don't use linux but the usual error on linux is the trivial case of upper/lowercase in a filename which linux is sensitive with but windows will ignore. 



So the first thing you will need is the right version of compiler which for Baremetal AARCH64 is ends in our target detail ARCH64-ELF.  That detail comes from this site

[]: https://www.linaro.org/downloads/



### CROSSING FROM WINDOWS INTEL PC:

You will need the latest file for the link below

><b>COMPILER:</b> https://releases.linaro.org/components/toolchain/binaries/latest-7/aarch64-elf/
>Download the i686-mingw32_aarch64-elf.tar.xz (yeah the biggest one)
>
>For the windows make executable
>
><b>Make:</b> https://sourceforge.net/projects/ezwinports/files/
>download "make-4.2.1-without-guile-w32-bin.zip" and set the extracted executable on the command line enviroment path


### CROSSING FROM RASPBIAN ON ARM PI3 or PI4:

<b>COMPILER:</b> 

I have no luck finding where you get the file from  but it will be called

 arch64-arch64-elf for 64 bit Raspbian and  arm-arch64-elf for 32 Bit raspbian

<b>Make:</b>

Will already be installed 



# STEP 1:  EDIT THE MAKEFILE

>
>The make file contains a path to the compiler directories and the prefix of the executable up to the -gcc in a variable called **ARMGNU**
>
>An example: ARMGNU = D:/gcc_linaro_7_4_1/bin/aarch64-elf
>
>That directory needs to reflect where **YOU** extracted the compiler to on **YOUR MACHINE** and you must edit it before you attempt to do anything.
>
>
# STEP 2: OPEN A COMMAND LINE
>
>Now change directory to the directory that holds the makefile, then use the commands below and type the parts in bold
>
# STEP3: THE MAKE COMMANDS
>**make clean** ... Cleans up all intermediate files, you need to do this when you make major changes to files.
>
>**make** ... This will launch the compile process and if you got your path right will work.

>

# THE HAXX: PREBUILT

>Yes I compiled each sample and it is provided in the "diskimg" directory of each sample directory. Simply take a formatted SD card and place the files in that directory onto the root directory of the SD Card place in Pi and turn on. 