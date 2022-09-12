# lineage-ir2mouse

Converts IR remote button presses to mouse movements or swipes.

For example, on a Rpi/PINN/Lineage setup used as a media centre.

As of Magisk 25.2, install ir2mouse and ir2mouse.conf as a boot scripts to /system/adb/post-fs-data.d (remember to set ir2mouse root X permission after copying).

Compass buttons move mouse or swipe, OK to click.
User assigned 'IR_MODE' button toggles mouse/swipe.
1-9 and 0 buttons change pointer movement/swipe factor.
