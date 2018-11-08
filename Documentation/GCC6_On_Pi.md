# Install GCC 6 on Raspberry Pi
>
First the warning I am a Linux newbie and I have no way to know if these instructions fail if they won't toast your entire linux install so BACKUP BEFORE YOU BEGIN. You will also probably need to do this on a 16GB SD card I am not sure if it will fit on smaller cards.
>
So I started with a new version of Raspbian Jessie (in my case
2017-07-05-raspbian-jessie.img) which I wrote on the SD card using the normal image writer. Then I started the system.
>
From there make sure Jessie was updated and upgraded
>
>1.) sudo apt-get update
>
>2.) sudo apt-get upgrade
>
I couldn't find any text editors I knew so next I installed VIM
>
>3.) sudo apt-get install vim
>
The prebuilt GCC6 on Debian requires stretch so we temporarily change repository source
>
>4.) sudo vim /etc/apt/sources.list
>
Change jessie to stretch in the repository source line then hit the esc key, colon key ':" and x which will save and exit the file in VIM.
>
Now we need to run updates for stretch
>
>5.) sudo apt-get update
>
Now install GCC 6 but will will put it under the extension "-6" so that the existing 4.8 GCC compiler in Raspbian remains.
>
>6.) sudo apt-get install gcc-6 g++-6
>
Now we need to put the repository back to Jessie
>
>7.) sudo vim /etc/apt/sources.list
>
Change stretch back to jessie in the repository source line then hit the esc key, colon key ':" and x which will save and exit the file in VIM.
>
Then again do a final update check
>
>8.) sudo apt-get update
>
If you got here it should be done. To check on a terminal command box type GCC-6 and hopefully you get the error message you didn't nominate a source file and you are good to go.
>
So the command GCC is the old 4.8 Compiler and GCC-6 is the newer version 6 compiler.
>
Now if your Pi is booting and running on the SD card to make a baremetal card you will need a USB to SD card reader/writer because you have the Raspbian card in the only slot. Once you have the SD card mounted via the USB you can copy the files you need onto it. Then you turn off power remove the Raspbian SD card and place your Baremetal card in the SD slot and power the Pi up. All being well your baremetal code runs and does what you expect :-) 
