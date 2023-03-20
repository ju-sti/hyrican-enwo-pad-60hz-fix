# Enable 60Hz screen refresh rate on Hyrican Enwo Pad, Study Pad One and Pipo W12

The Hyrican Enwo Pad (also known as Hyrican Study Pad One and Pipo W12) tablet has a big flaw. The very nice 3000 x 2000 Pixel 12.3 inch display is only capable of refreshing itself at around 37 Hz (according to testufo.com).

## How to fix this problem
1) **Disable Bitlocker first!**
2) Disable Secure Boot in the UEFI setup. The easiest way to get to the UEFI is to open a cmd.exe terminal and enter ```shutdown /r /fw /t 0```
3) Download the file ```ACPI_DSDT_Override.reg``` and start it in Windows.
4) Open a cmd terminal as admin and enter ```bcdedit /set testsigning on```
5) Restart Windows. 

## Known issues
1) Only tested by myself. If your device hardware is different from mine this fix could completely disable your Windows (bluescreen when starting).
2) Sometimes the refresh rate will only change to 60Hz after turning the screen off and on in Windows.
3) Sometimes changing the screen brightness doesn't work.
4) It's necessary to turn the screen off and on again once after starting Windows to enable the fix.
5) Ugly test mode overlay on the desktop because of the testsigning mode.

## How does the fix work
The Qualcomm display driver reads a panel config from the DSDT ACPI table. With that configuration it configures it display output and also configures the DSI to eDP bridge chip. The fix removes a configuration option which is optional. After removing this DSIBitClockFrequency entry the graphics driver automatically calculates the DSI data rate for 60fps itself using the existing DSIRefreshRate configuration entry.
The easiest way to override the ACPI tables is by using the ACPI override using the Windows Registry and testsigning mode.

## Do it yourself
1) Download the zip with acpidump.exe and iasl.exe from https://acpica.org/downloads/binary-tools
2) run ```acpidump.exe -b -n DSDT```
3) open DSDT.dat with a hex editor (e.g. HxD), search ```DSIBitClock``` in open file
4) replace the string ```<DSIBitClockFrequency>700000000</DSIBitClockFrequency>``` with whitespaces (hex 0x20) to remove this configuration option
5) Increase the OEM revision ID number: change 0x03 to 0x04 at position 0x18
6) save the edited file
7) run ```iasl.exe -d DSDT.dat```
8) open the dsdt.dsl file and look at the corrected checksum ("...should be...") at the top of the file
9) replace the existing wrong checksum with the new corrected checksum in DSDT.dat, it is stored in the first row at position 0x9, save the file
10) Download and install the WDK with asl.exe from https://learn.microsoft.com/en-us/windows-hardware/drivers/bringup/microsoft-asl-compiler
11) Run ```asl.exe /loadtable -v DSDT.AML```, see for more details https://github.com/bentiss/SimplePeripheralBusProbe/blob/master/README.md#overloading-the-dsdt
