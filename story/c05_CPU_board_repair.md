I had the PSU "freshened" and the monitor and terminal were working, so I went to testing the CPU board.

Initially it all seemed OK, it didn't have any disk or floppy attached so it printed errors when trying to boot.

At that time I didn't have the disk archived yet but I did have the ZuluSCSI emulator and the Gotek floppy emulator (loaded with FlashFloppy) and I had a couple images of floppies that were supposed to be compatible with this "early" version of this computer (text terminal, no graphics). The only disk image I could find on the internet was for the later graphical version, so I didn't expect it to work.

The first hurdle was to find the correct image parameters for the floppy emulator. After some searching I found the original user manual for the floppy drive that came in the computer, a Panasonic JU-465, which said it was a 2-sided, 80-track, 18 sector/track, 256b sector drive.
Other sources (computer's service manual) said that it was 77-track with a sector interleave 2.
Computing some values and comparing them to images I had downloaded, I saw that this matched for some images I had, but some were just with 73 sectors. Anyway, I created the corresponding IMG.CFG for FlashFloppy for both of them and tried booting.

No success - it didn't even try booting from the floppy, it just said "floppy malfunction".

Then I tried commenting out sector interleave (leaving it at the default of 1).

Partial success - it started booting "CP/M V3.0 Loader" but didn't get any farther as it froze.

I tried different things like `image-layout = sequential` or `id = 0` but both were worse as they weren't even recognized.

Then the system even stopped loading the ROM. It didn't even print "TESTING MEMORY..." as usual which is the first thing it does. I unhooked everything but it stayed the same, so something on the CPU board had certainly died.

I thought about what it could be and measured different points, mostly around the general stuff - clock was there, reset was normal, supplies were normal. But BUSRQ- was low (active) and BUSAK was active, which meant the CPU was held offline. This was supposed to only happen during a DMA cycle, so I measured the DMA chip, and it was indeed putting out the BUSRQ signal.

I thought maybe this was some fault in the code, maybe something was wrong with another part, like the ROM, or the code was getting corrupted when read, or there was something else that the DMA was trying to access that didn't work. I probed around with the LA for a while, measuring inputs and outputs of gates around the CPU and DMA while rebooting the board. I couldn't find any anomalies, and I could see that the DMARQ line went active immediately after power-on, while the system was still in reset. It couldn't be anything else but the DMA chip itself.

I took out the CPU board and desoldered the DMA chip (with just a hand pump! still got it out with no damaged traces or pads at all) and installed a socket.

Sure enough, after trying it again, it now booted from the ROM and tested memory! It even tried to load from the disk, but of course that wouldn't work as the DMA chip is removed (disk and floppy data transfers are done with DMA in this ROM version, even from the ROM).

So I had to order a replacement DMA chip. I found a seller on ebay that had not only the DMA, but also SIO and PIO chips that could be added as options to the board that I didn't have.
I ordered two versions of the DMA chip - one made in the DDR by MME (RFT) marked "80A DMA" and another Zilog Z8410APS (Z80A DMA).

After receiving them I tested them and they all seemed to work, and yes, I was back to freezing at "CP/M V3.0 Loader".

At this point I thought maybe something was wrong with reading from the floppy or the Gotek.

(contined in the next part)
