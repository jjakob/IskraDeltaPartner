In the last chapter I tried to boot from a floppy from the Gotek loaded with floppy images I got from the internet. Since those didn't boot, I thought maybe there's something wrong with the floppy read circuitry or the images were incompatible.

I couldn't lose much by trying to boot from the (very likely incompatible) disk image "PartnerGBootUp.img" using the ZuluSCSI.

This quickly revealed a problem. Even though there was a "Xebec" quirks setting in the ZuluSCSI, it did not work at all. It didn't even try to read anything, but reported a disk fault immediately.

I loaded debug firmware onto the ZuluSCSI to see what was going on. This logged debug messages to a logfile on the SD card.

The problem was obvious. The ZuluSCSI didn't understand the command the computer was sending it. Looking up what command 0x0C in the S1410 manual revealed that this was the "Initialize Drive Characteristics" command. This command tells the Xebec controller the parameters (cylinders, heads, ...) of the attached disk drive, since it doesn't store those on the disk itself, it has to be configured by the host every time it's powered up.

The ZuluSCSI didn't have any code to handle this command, so it just returned an error status when it received it.

I added code to handle this command and print the received disk parameters to the log, just to check what I think are the right parameters are actually right and that my system didn't have some oddball ROM or something.

There was some work to set up the build environment for ZuluSCSI, they use PlatformIO, I didn't want to litter my system with it so I set up a minimal Dockerfile based on Devuan that installed PlatformIO. This also gave me isolation from this unknown code and my personal data.

After building it and testing, I found that it worked and now read from the image and started booting! But it soon also froze, but now at a later point, as it already started to load CP/M and printed "TPA 61K".

I didn't expect it to boot, as the image was for the graphical version of this machine, mine didn't have the graphics card. I still didn't know whether or not there was a fault on the CPU board or I just didn't have a compatible image. I had to have the original disk image the system came with to be sure.

Continued in the next part.
