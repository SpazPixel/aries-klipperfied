!!!Safety Warning: Do Not Touch Live Electronics!!!

Prerequisite: install [srecord] to Windows (https://srecord.sourceforge.net/download.html) (if installing srecord to a non-default directory, "to-hex.bat" will not work out of the box.)

Prerequisite: install [Klipper](https://www.klipper3d.org/) host software to a device of your choosing

Download this repo as .zip, extract all files and move to the root directory of a fat32 a USB drive.

**Make sure the usb drive shows up in your printer's menus before continuing.**

Run "make menuconfig" on Klipper host with settings shown in makemenuconfig.png

Note, 12Mhz clock only works if "klipper/src/stm32/Kconfig" is modified with the following:
```
    #default 128000000 if MACH_N32G45x # old line
    default 144000000 if MACH_N32G45x  # new line
```
If you're uncomfortable with/don't know how to modify this file, use "Internal Clock".

Run "make" on Klipper host.

Drag resulting "klipper.bin" onto root of USB drive.

Create a copy of "klipper.bin" called "firmware.bin". (Keep both files at root directory)

Edit "to-hex.bat" to your usb root directory.

Run "to-hex.bat" on Windows. you should see a new "firmware.hex" file was created.

Plug drive into printer, turn printer on.

You'll see progress images come up on-screen.

Firmware files will be automatically flashed to stm32 board via voxelab's built in programming tool.

!Unplug printer and wait for residual power to drain!

Open bottom panel of printer.

Connect Klipper host to printer via configured UART pins (see "pads.jpg").

If you know what you're doing, you may want to solder some Dupont style pins to the UART pads (a 2-gang of pins from your average microcontroller works perfectly if you bend the small side to fit in snugly).

Suggested you unplug either the ribbon cable connecting the screen board to the display, or the ribbon cable that connects the screen board to the n32 board.

Close bottom panel securely and power on.

Adjust "printer.cfg" to reflect your Klipper host's communication device (usb, serial).

Upload "printer.cfg" to Klipper host.

Ensure your slicer sends the correct macros defined in "printer.cfg".

Reverting to stock firmware is as easy as booting the printer as normal. un-solder uart pins, plug back in any cables you may have unplugged.

You'll get a prompt on-screen stating something akin to "The firmware failed to update. Press OK to retry", with an "OK" button.

Once you press the button, the LCD board will flash the original firmware to the stm32 board, you'll be able to use it as normal.
