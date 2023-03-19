# Enable 60Hz screen refresh rate on Hyrican Enwo Pad, Study Pad One and Pipo W12

The Hyrican Enwo Pad (also known as Hyrican Study Pad One and Pipo W12) tablet has a big flaw. The very nice 3000 x 2000 Pixel 12.3 inch display is only capable of refreshing itself at around 37 Hz (according to testufo.com).

## How to fix this problem
1) Disable Safe Boot in the UEFI setup. The easiest way to get to the UEFI is to open a cmd.exe terminal and enter ```shutdown /r /fw /t 0```
2) Download the file ```ACPI_DSDT_Override.reg``` and start it in Windows.
3) Open a cmd terminal as admin and enter ```bcdedit /set testsigning on```
4) Restart Windows. The refresh rate will be 60Hz after turning the screen off and on again.

## How does the fix work
The hardware configuration of the display panel is changed. Actually it is the configuration of the DSI to eDP bridge chip in the tablet but I'm now to tired to write more about this after working the whole weekend on this topic.
