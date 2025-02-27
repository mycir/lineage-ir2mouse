# lineage-ir2mouse

Converts IR remote button presses to mouse movements, swipes and navigation keys.

For example, on an RPi/PINN/Lineage setup used as a media centre.

Install ir2mouse and ir2mouse.conf as boot scripts to an appropriate location. In [Magisk](https://f-droid.org/en/packages/com.topjohnwu.magisk/) 25.2 this was /system/adb/post-fs-data.d but, as of Magisk 28.0, /data/adb/service.d is the recommended location. (Remember to set the ir2mouse X permission after copying.)

Reworked, with enhancements, February 2025:

IR scancodes and Android keycodes are user assignable in ir2mouse.conf.

Compass buttons move the mouse pointer, swipe, or simulate navigation keys - OK to click.
0-9 buttons change pointer movement/swipe factor.

'IR_MODE' cycles mouse/swipe/key navigation.</br>
'IR_ENABLE' toggles the ir2mouse enabled state when using lirc aware apps, such as [Kodi](https://kodi.tv/).</br> 
'IR_FULLSCREEN' activates a registered app's fullscreen mode.</br>
'IR_PLAY_PAUSE' activates and taps a registered app's play/pause button. Otherwise it is sent as an Android keycode.</br>
'IR_ROTATE' toggles portrait/landscape, which may force a misbehaving app to the correct aspect ratio.

Various other media control and other Android actions are defined in the example ir2mouse.conf, which could be extended as required.

An app is 'registered' by adding its ID and activity string to ACTIVITIES in ir2mouse.conf. You must also add the coordinates of its fullscreen control to FS_TAP_COORDS. So, by example:

ACTIVITIES="\<app1> \<app2> \<app3>" and FS_TAP_COORDS="\<app1_fsc_x,y> \<app2_fsc_x,y> \<app3_fsc_x,y>".

Finally, there is now an option to receive confirmation of mode and enabled state changes as Termux toasts.

## Setup help

Before moving ir2mouse and ir2mouse.conf to your boot scripts location, try them in /data/local/tmp, set TERMUX_TOASTS=0, then launch from the adb shell.

To determine your keyboard layout file:
```
adb shell dumpsys input | grep -A20 "Keyboard"
```

To determine ideal t_repeat values in ir2mouse.conf (see comments therein) for mouse buttons, play around with them in such as the [Total Commander](https://www.ghisler.com/ce.htm) editor, then relaunch. NB Ensure that any VNC client is disconnected before doing this.

Alternatively, you may find it more convenient to edit ir2mouse.conf on your PC, then launch two terminal windows. One to push changes:
```
adb push -a -p "/path/to/ir2mouse.conf" /data/local/tmp
```
Then relaunch from your other terminal window:
```
adb shell
$ su
# /data/local/tmp/ir2mouse
```
To obtain the '\<app ID>/\<current activity>' when registering an app, activate it, start playing something, then:
```
adb shell dumpsys activity activities | grep -A20 "topResumedActivity"
```
To obtain its fullscreen control coordinates:

Settings > System > Developer Options > Pointer location.

Note the coordinates when clicking the control's centre.  






