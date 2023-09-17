My computer is the older "text" version that only had a built-in serial terminal, with no graphics capability (as much as a pretty dumb 80x24 terminal at 9600 baud has).

This terminal is a completely separate, standalone board, which has a completely standalone processor system on it, complete with CPU, ROM, RAM, DMA, PIT, UART and CRTC.

Since there were no schematics available for it, I decided to [reverse engineer it](https://github.com/jjakob/IskraDeltaPartnerVideo).

The basics are: it's a terminal with two serial ports, one for the keyboard at 300 baud, and another for the computer at 9600 baud. Its protocol is pretty dumb, it supports absolute cursor positioning, inverse video, blinking, separate status and date fields on line 26 (under the main 80x24 display field).

There is no setup menu that I know of. All characters coming from the keyboard at 300 baud are sent as-is to the computer at 9600 baud. Serial characters from the computer control the display.

The hardware has support for much more than it's capable of with the stock ROM, including program and character ROMs of twice the size (4k), 4 character sets in the character generator ROM, RS-232 serial with hardware flow control to the host instead of just TTL Rx/Tx. I imagine a VT100 compatible terminal could be made with new software.

I decided to do a couple mods to it, not because of necessity but just to see what I could do.
- populate the connector for RS-232
- add a switch to select between RS-232 and TTL (external/internal) host connections (which would be useful to use it as a terminal for something else, not just the built in computer)
- modify the composite video output section to correct PAL video levels
- make the HLGT (highlight output on the CRTC) work on both TTL and composite monitor outputs (the stock ROM doesn't support this, but a new ROM could)

Details for all the mods are in the schematic.
