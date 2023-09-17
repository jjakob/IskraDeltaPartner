After imaging the original MFM drive and successfully getting CP/M to boot from the image using ZuluSCSI, I ran into another problem.

After it was on for anything more than just a minute, it would not boot after a reboot any more. It didn't matter whether it was a hot or cold reboot. It only booted again after at least 10 minutes of being off. This immediately turned my suspicion to a thermally related fault on either the CPU or SASI board.

First I tried cooling down individual chips using a can of butane lighter refill turned upside down. (only do this in a well ventilated area or you might literally set yourself on fire!) I cooled down a couple chips at a time (2 to 3) and hot rebooted with the reset button. I went through the entire CPU and SASI boards with no success.

I even went through this cooling process 2 more times, just to be sure, the last time with the power switch, not just reset button, like before.

The very last chip I tried was the DMA, since I didn't think it was bad, I just replaced it! But as I cooled the DMA with the liquid butane and power cycled the computer, it booted!

Turns out it was the new (old stock) MME 80A DMA chip! I didn't catch it before because I wasn't suspecting it, and it probably wasn't enough that I just used the soft reset button, it had to be hard power cycled to come back to life.

I swapped it with the Zilog DMA chip I had also ordered (just in case something like this happened, or the MME chip was incompatible, since it is a clone, not the real Zilog part). It worked. It continued working for an hour and many reboots. It still works to this day.

Now that I knew that chip was bad, or maybe just didn't like working at 4MHz (even though the 80A should work at it), I wanted to see if all of the MME chips I had acted the same. Maybe I just had a dud and the others were good. I had 4 so I could try.

The 2nd MME chip initially worked. I rebooted fine even after minutes of power-on time (something the other MME chip couldn't do). But it also failed after a couple hours. I put the Zilog back in and didn't even test the remaining 2 MME chips. Maybe they work better in some other system, or at a slower clock speed, but I conclude they're incompatible with this computer.
