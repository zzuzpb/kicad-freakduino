The correct bootloader (binary HEX) to use with the KiCAD-Freakduino is
ATmegaBOOT_168_atmega328_pro_8MHz.hex. The copy residing in this folder was
taken from the Arduino IDE software at the time of writing.

Fuse settings for the ATmega328P in the KiCAD Freakduino are:

lfuse 0xe2
hfuse 0xda
efuse 0xff

For more information, see the note regarding bootloader location, size and fuses here,
http://www.freaklabs.org/index.php/Blog/Store/2013-03-28-Freakduino-Errata.html


