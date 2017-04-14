This is the Marlin v1.1 Release Candidate Bugfix firmware as of April, 27, 2016.

It is configured for the TEVO Tarantula printer, standard bed, with auto bed levelling.

Hot end and heated bed PID is enabled, you should run PID autotune.

The auto bed levelling has been enabled and configured for the TEVO Tarantula with a fixed sensor.

This release includes support for multiple extruders. It is not enabled as I can't test this feature.

Use at your own risk!

You will need to modify several settings in configuration.h for your specific printer:

Lines 474 to 476: Set your axis directions. They are currently set to match the build in Ed's videos. Should be fine for most, but some may need to change Y axis direction.

Lines 503 to 508: Set your bed dimension.

Lines 616 to 618: If you are using a Z-Probe, set your offsets here. You can leave the Z offset at 0, see comments about M851 below.

Lines 664 to 666: Set your home position offsets.

Note that EEPROM is enabled. If you do not wish to use EEPROM, comment out line 740.

If you are using Auto Bed Levelling and you have a fixed sensor attached to the hot end, you should be good to go (after making the changes described above. If you have some other kind of sensor (servo type, sled, etc) read the comments at lines 629 to 647.

Marlin v1.1 has implemented a new custom M code for the Z offset, M851. Syntax is M851 Z<offset> where <offset> is the difference between were the sensor detects the bed and the distance the nozzle is from the bed. It should always be negative for fixed sensor probes. To use follow these steps:

Do a G28 to home all axis. 
Do a G1 X100 Y100 to move the nozzle to the middle of the bed.
Send G1 Z0 to move the nozzle what it thinks is the correct nozzle height, which should be the same as where the sensor detected the bed.
Send G92 Z5 to make the printer think the current z posisiton is 5mm above the bed.
Place a piece of paper between the nozzle and the bed.
Use your host programs printer controls to lower the Z axis .1 mm at a time.
When you feel some resistance to moving the paper, make a note of the Z position in your host program.
Subtract 5 from this number. That is your initial Z offset.
Send M851 Z<number> to the printer.
Send M500 to save the offset to EEPROM.
Try a print.
If you need to adjust the Z offset because it is too close or too far away from the bed, simply send another M851 Z<number> with the new offset you want to try, followed by M500. Lather, rinse, repeat until you have the offset dialed in.

Note: due to various environmental factors, the Z offset can change from day to day. If you start a print on a new day and find the Z offset is not right, simply send M851 Z<offset> followed by M500 until it is good again.

Have fun!
...jim
