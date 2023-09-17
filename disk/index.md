The disk inside the computer was a Seagate ST-412. The factory manuals refer to it as "Winchester".

The interface between the CPU board and the disk drive has 2 parts: the SASI adapter and the Xebec S1410 MFM disk controller. They're mounted on the back of the computer on a metal plate with plastic standoffs.

The SASI adapter is connected to the CPU board with a 64-pin ribbon cable with unusual IDC connectors. This connector is labeled "J2 BUS" and carries a buffered Z80 data bus, address bus (just the lower 8 bits), Z80 control signals, DMA, IRQ signals and power.

The SASI adapter card only had documentation about programming it in the service manual but there were no schematics available so I [reverse engineered it](https://github.com/jjakob/IskraDeltaPartnerSASIAdapter).

The Xebec S1410 controller probably has a stock rev. F ROM.

I documented the process of archiving the ST-412 [here](../story/c07_disk_archiving.md).
