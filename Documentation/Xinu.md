# XINU .. Funny code that just makes you laugh

### uartInterrupt.c (ns16550 handler)
```C
for (u = 0; u < NUART; u++)
    {
        uartptr = &uarttab[u];
        if (NULL == uartptr)
        {
            continue;
        }
```
How fast did you spot it !!!!
>
uartptr is a pointer to a data table entry position in memory and the next test is to see if it is NULL.
The only possible way that could happen is u=0 and uarttab was at 0x0 on the vector table. The funny part of that
would be it would then fail when it shouldn't as a random bug.
>
Hey I am a normal coder and I am willing to bank uartptr is non zero and remove the test .. living dangerous :-) 



### Hey lets turn off the interrupts and again oh and again

So calls like yield and wait turn off the interrupts and then call for a reschedule
```C
syscall yield(void)
{
    irqmask im;

    im = disable();
    resched();
    restore(im);
    return OK;
}
```
Want to guess what the first lines of reschedule do .. you guessed it
```C
 throld->intmask = disable();
 ```
 This is a pattern that is repeated multiple places and as I tried to get multicore online drove me nuts.
