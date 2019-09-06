## NXPProg

Programmer for NXP arm processors using ISP protocol.

For help run the command with no arguments:

```
./nxpprog.py
```

Program image file to processor:

```
./nxpprog.py <serial device> <image_file>
```

The image start address defaults to 0.
When the image start address is 0 a checksum is inserted in the reserved
interrupt vector so that the bootloader will boot the image.
The image file is a raw binary file (output from objcopy -O binary).

Note:
Xonxoff flow control does not work with some usb serial
converters on windows and doesn't seem necessary in my setup.
If you in your setup need flow control, for example
if you get programming errors, then try enabling this.

## Windows Advice

When you have installed python for windows and the (py)serial module
then something like this should work:

```
<path to python>\python.exe nxpprog.py COM1 image.bin
```
It is very important that the serial port name is written in capital letters;
lower case names will not be matched against possible serial devices.

## Changelog

### V2.3 
- Fixed [corruption issues with FTDI adapters on Windows](https://github.com/pyserial/pyserial/issues/394)
- Added some internal debugging options
- Improved resilience against data corruption errors
- Removed unneeded ihex file type option (I think it was causing problems but I can't remember why)

### V2.2

Minor update.

Added better data for LPC 1817.
The newer versions need to have the devid word 1
masked as the higher bits are the flash size encoded.

### V2.1
Minor update.

Added data for LPC 1817.


### V2.0
This is a major update.
The scripts are converted to python 3, python 2 is no longer supported.
Support has been added for NXP 18XX cortex M3 based SOCs.
Checksum calculation for the cortex based processors has been fixed.
