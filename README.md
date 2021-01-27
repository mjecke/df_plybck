# DF PLYBCK
Eurorack DF Player based sampled playback module.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.


![DF PLYBCK](/DFPLYBCK.jpg)

This is a module designed to use the DF PLAYER, a simple audio playback module that plays files direct from a microSD card.  
The original DF module details are here: https://wiki.dfrobot.com/DFPlayer_Mini_SKU_DFR0299

The modules I purchased for testing all came from eBay at around $2 a unit; there may be different clone versions out there, and I do not know if they are all compatible.

This module is experimental and had build quirks. The PCB has various unused and untested parts. I don't have a schamtic at this time but see the pcb layout below to help with the build and read these notes.

## TIPS TO BUILD:
See PCB- DF Player is soldered directly to PCB.  

When assembling, solder BUSY LED first before soldering DF module. I don't think the LED polarity is marked, check it to ground before soldering.
Assembly all jacks and microswitches and the pot loose first, install into front panel, then solder.  
Then assemble the DF Player module and use a micro SD card in slot to ensure slot is aligned with front panel, then solder DF playe at correct height above PCB. The DF player pins should just reach the back of the PCB at the correct standoff distance.

I used the module with a 16 pin power connector as I have 5V power in the rack.  Alternatively, I laid out a 5v regular as optional if you want to only install a 10-pin power. Just do not populate a 7805 if you use a 16 pin connector!

There is an 'expand' section of pin headers that tap into pins on the player for potential expanders.  They are unused now.

Do not place the 2N7000 or the 820k resistor as that was to experiment with triggering differently.  
Where there is a jumper for "hi z trig" or "direct trig", place a jumper wire for the direct trig.  

This module will trigger with a 5V gate straight into it- but note it only triggers on a low-to-high AFTER being pulled high then low one time.  Thus it will clock to a 5v gate to play short samples (like a hi-hat) in time but not off the first pulse.  It plays with relatively low latency if the file it is playing is small.  
WARNING - the trigger input is direct and I have NO PROTECTION on this version;  Consider adding a 5.1V zener as a clamp diode in the place where the 820k resistor silkscreen is. Or just do not give the trig input signals over 5V.  I think it was OK with negative 5v swings on a square lfo I gave it, but unsure.  The IC likely has clamp diodes internally to protect against anything over 5v but I did not do tons of testing.


## HOW TO USE:
The module only plays files off the root directoy of the microSD card.  I suggest using a small SD card and formatting it for FAT32.  Then number files 01.wav, 02.wav, 02.wav etc.  You can play through them in order with the buttons. 

The FILE select potentiometer does not work all that well- it is sending an analog voltage that maps to files between roughly file # 4 and file # 10-14 on the device.  It could use some tuning in value with a ganged resistor maybe.  I just put various files into different numbered positions on the SD card between 04.wav and 10.wav and it would select... some of them, sometimes.  It is quirky, but fun.

The TRIG input likes a 5V Gate and if you have a short sample it will clock to it pretty well.  

Sometimes you have to pause/play to get it going.  It will play a sample out to end.
If you hit loop it will loop that one, I think you hold it to stop. See the DF Player wiki for more info.


## Basic BOM:

QTY | PART
------------ | -------------
1 | DF Player Mini
3 | PJ302M jacks
1 | TL072 opamp
1 | 2N3904
1 | 3mm LED
5 | 6X6X9mm DIP Right Angle Microswitches 
1 | A100k logarithmic potentiometer, right angle, 9mm alpha style
6 | 1K resistors
2 | 5k trimpots (3296 style) or 3.9k resistors  
2 | 18p ceramic caps for output HF filtering
2 | 10uF electrolytics 
3 | 100n ceramic caps
1 | 51K 1% resistor (value is important)
1 |33K 1% resistor (value is important)
1 | 2.54mm power headers
Optional | 7805 TO-92 5v regulator

Ignore 2n7000 and 820k resistor on PCB

Note this module uses micro SD cards, however for brevity the front panel design just says 'SD CARD' over the slot. 

## PCB Layout:
Silk / Front / Back
![DF PLYBCK](/df_plybck_PCB_layout.png)
