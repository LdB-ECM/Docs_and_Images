# Compiling Xinu for hard or soft FPU #

The original Xinu context switch code was strictly for soft FPU implementation in that the context switch and the interrupt code only saved the general 16 registers (there was also a warning about R13 which was okay to ignore). The new code pushed allows that original mode by using the flags -mfloat=soft or many (perhaps most??) versions of GCC setup for that unless you specify FPU flags. That is the code compiles in the historic original soft FPU mode under those situations.

The new code allows you to specifiy the FPU hardware type and the standard flags -mfloat=hard which will then add saving the FPU registers to the context switch and the interrupt handler as well as slightly modify the stacksetup. In theory it will do that automatically as GCC should push predefined macros it uses. However with so many variants of GCC out there it is hard to be completely sure, so any bugs please open a ticket.

In Hard FPU mode a full register push is 50 registers as Xinu context switch is lazy. So the context switch is technically slower but the running code especially if it uses the FPU is usually much quicker. So you can choose which of the modes you wish to use. Currently I have put the FPU mode compiled in the startup message to the screen.

You change the mode in the file compile/platforms/arm-rpi/platformvars it conatins the entries above

#### However if you change settings you must do "make clean", "make libclean" and then a "make" ###
Basically you must clean all existing object files that were compiled with the FPU in a different setting.

The files changed for this feature
1. /loader/platforms/arm-rpi/start.S
2. /system/platforms/arm-rpi/ctxsw.S
3. /system/platforms/arm-rpi/irq_handler.S
4. /system/platforms/arm-rpi/setupStack.c
5. /compile/platforms/arm-rpi/platformVars

I will be looking at doing not lazy context switches but I also need to alter the way the interrupts are working. The original interrupt code is firstly only IRQ based there is no FIQ option and secondly really designed for single core. Basically the interrupts are handled by whatever core is given the handler function. On a multicore system we need the ability for the core the IRQ is routed to mark the irq as needing service but one of the other cores to actually handle the interrupt if required.

I have several different multicore designs in mind and even on the current code you can sort of start playing. If you route the timer to another core and then use the CoreExecute function in the start loader you can get Xinu to run as is on another core. All the cores are parked ready to go and you just send it to "main". I was considering doing a really basic implementation but the queues in xinu are largely created thru a series of macros (open queue.h). I have little faith I can work out a way with to make that thread safe, so current plan is redo the queue and in that new code allow different priority options.
