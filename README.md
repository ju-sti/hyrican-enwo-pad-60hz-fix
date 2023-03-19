# Enable 60Hz screen refresh rate on Hyrican Enwo Pad, Study Pad One and Pipo W12

The Hyrican Enwo Pad (also known as Hyrican Study Pad One and Pipo W12) tablet has a big flaw. The very nice 3000 x 2000 Pixel 12.3 inch display is only capable of refreshing itself at around 37 Hz (according to testufo.com).

## How to fix this problem
1) Disable Safe Boot in the UEFI setup. The easiest way to get to the UEFI is to open a cmd.exe terminal and enter ```shutdown /r /fw /t 0```
2) Download the file ```ACPI_DSDT_Override.reg``` and start it in Windows.
3) Open a cmd terminal as admin and enter ```bcdedit /set testsigning on```
4) Restart Windows. The refresh rate will be 60Hz after turning the screen off and on again.

## How does the fix work
The hardware configuration of the display panel is changed. Actually it is the configuration of the DSI to eDP bridge chip in the tablet but I'm now to tired to write more about this after working the whole weekend on this topic.

## Known issues
1) Only tested by myself. If your device hardware is different from mine this fix could completely disable your Windows (bluescreen when starting).
2) Screen brightness can't be changed (I will fix this soon)
3) It's necessary to turn the screen off and on again once after starting Windows to enable the fix.
4) Ugly test mode overlay on the desktop because of the testsigning mode.
