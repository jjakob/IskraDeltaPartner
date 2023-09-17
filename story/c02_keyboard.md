Since I didn't have a keyboard, I asked on the forum (the biggest forum for electronics in our country) whether anyone had a keyboard for it. Someone said they did, and on pictures it looked kind of like it would fit. But as I bought it and it got to me over post I saw that it was not right. It had a DB-15 connector and was parallel. It had a sticker saying it was for the "HR-84" computer, which was another Slovenian computer, but completely different.

So I forgot about it as I couldn't find a keyboard anywhere.
Until years later when I happened to remember about it and search for it again, I found someone selling one that looked like it was correct and had the right plug on it (6.3mm TRS jack). I got it home, cleaned it up, but didn't have time for it, and the computer was still in storage, so it also got put into storage next to it.

In 2023 as I decided I wanted to finally do something with this computer, at least archive the data off it, pulled it and the keyboard out from storage, and as I like to do, instead of just plugging it in and trying it, I took it all apart to first understand how it works.

It's based on a 8048 processor with an external EPROM.
It has a bidirectional serial UART interface with the host system at 5V TTL levels.
On this particular keyboard it was only fitted with a 3-wire cable and TRS jack, so it could only send data one way to the host. I connected it to my Linux machine with a FTDI USB-serial adapter, and as I found from watching the data line with the oscilloscope, received data from it at 300 baud, 8 data bits, no parity, 1 stop bit.

I could also send data to it and it would cause it to beep, but that was pretty much it. I didn't have any documentation on the receive side of the protocol, so I played around with setting and resetting different bits on it until I found only the first bit controlled the buzzer, the rest I suspected controlled the LEDs.

I only suspected that because my keyboard didn't have LEDs fitted, nor did it have the chips that drove them.

I searched and found the schematic for it (on the same forum mentioned above) which was for a "Paka 3000" which is apparently the same as for this computer. It also revealed the chips I needed for the LEDs were a 74LS374 and a 7406.

I found a 74C374 and 7405 in my junk board pile and after desoldering and cleaning, installed them in the board.

Now I could see the outputs of the 374 changing state as I sent the keyboard data, and I found out the mapping from data bits to LEDs.

I measured and drilled 8 holes in the case that aligned with the LED locations on the PCB.

After searching for and barely finding 8 5mm LEDs in my parts drawers and junk pile, I installed them and their corresponding resistors. First putting all the LEDs into the board loosely, then putting the PCB into the case, pushing the LEDS into the case holes until they aligned flush with the top of the case, and soldered them in.

Then I decided to change the original 3-wire cable to a 4-wire, so I could maybe use it in the future with something else other than the computer it was meant for.

I drilled and filed a hole for a 6P4C jack on the back of the case, glued it in with epoxy and wired it to the board.

I modded the keyboard with some protection for the power and data lines, in case someone plugged it into a phone line or something else potentially damaging.

On the +5V power rail a 1.5uH inductor to act as a fuse.
On the TX line a 100uH inductor and 100nF cap to GND, and a 680 ohm pull-up. The LC low-pass still passes 300 baud serial with no problem, but substantially limits the radiated EMI from what would otherwise be a high-speed digital line (not much EMI compared to the completely unshielded main CPU board, but I digress).
On the RX line nothing? It might be good to put some protection there too.
