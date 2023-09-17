The power supply was all original.
Since there was more noise on the power rails than I liked, and I could see some shimmering on the CRT that I suspected was from this noise, I decided to take a deeper look at the power supply.

Luckily I could find a schematic for it, even though it was a very low resolution scan, it was just barely good enough to read.

I opened the power supply, discharged all the caps (especially the primary main filter cap) and measured their capacitance and ESR. They were all in spec.

Looking at the schematic I saw there was no feedback loop compensation which I thought was very odd, as all power supplies with this topology (half-bridge isolated buck converter) needed it.

I read about how to calculate the values for a compensation network, and after a lot of reading, could finally find an appnote that had formulas that allowed me to calculate it.

Still, the feedback network topology was different in that appnote (inverting feedback amplifier) versus in the TL494 (non-inverting feedback amplifier) but I thought that as long as I went on the safe side (overcompensated) it would be OK. It was designed with no compensation at all, any compensation would be better.

Plugging in the values for switching frequency, switching voltage, output inductance, output capacitance and ESR (for the new, not old, capacitors), I arrived at values of:
`R7 = 18p || ( 2n2 + 330k )`. That's 18pf in parallel with (2n2 in series with 330k). R7 needs to be removed and these 3 components put in place of it (see picture for detail).

These also need to be replaced:
R4=22k
R6=330k
R5=22k

C1 and C4 need to be removed.

I replaced the output capacitors with two new low-ESR in parallel, which gave an even lower ESR. The total capacitance is less than the original, but I calculated the needed capacitance for this switching frequency and desired output ripple is only 12uF! The originals were so high in capacitance just to get a low enough ESR, as very low ESR capacitors weren't available in the 80s.

For this I drilled holes to mount the two radial caps flush onto the board and connected them with thick wire on the bottom of the PCB. This way they're very securely mounted and don't move around at all and can't come detached with mechanical impact.

The primary side snubber RC were overheated and discoloured. The originals were 220 ohm 0.5W carbon film in series with 1nF 400V. I replaced them with 51 ohm 2W metal film and 4n7 1KV ceramic disc.

Before powering up again, both voltage trimmers need to be set to the minimum voltage, as the changes in feedback resistors mean it might regulate at a slightly different voltage than before.

Power up with loads on +5 and +12 rails (I used car light bulbs).

Then adjust output voltages for +12.1V and +5.15V (there is no remote sensing so some voltage will get lost on the wires, this gave me pretty close to 5.0V on the logic boards).

I didn't adjust the current limit pots as I didn't modify any current feedback parts and those trimpots were still factory sealed.

Everything checked out fine, including output ripple which was lower than before.

I also tightened all the female contacts in the power connectors as some were pretty loose.
