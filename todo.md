# DualPanto issues and plans
## Unreliable Instances
These are the issues that we observed in class last year and do not know the cause and how to fix (in decreasing severity):

- does not connect reliably (when this happens, 40-80% of the times when Unity starts, dualPanto fails to connect)
- disconnects after pushing hard into an obstacle
- disconnects after turning on the power
- obstacles do not render when there are too many obstacles
- having moving obstacles that enclose the godObject and pushing it makes it unreliable
- “sliding” sensation when touching corner of a cube
- “switch to” didn't work in some cases (might be an issue with student's unity implementation)
- some computers cannot detect/communicate with dualPanto, while the same dualPanto works with other computers
- obstacles don't clear up after switching levels
- the firmware should be uploaded from the same computer running Unity. Otherwise, a user feels a force from all directions (feels like put finger in honey) after touching wall or force field

## The Faulty PCBs
We also had 11 broken PCBs and these are their current states:

- cannot upload firmware and does not send heartbeat through serial (1/11)
- firmware uploads, but does not send the heartbeat correctly (doesn't send “start” msg, subsequently no useful connection) (2/11)
- firmware uploads, with other connection issues (1/11)
- encoder not tracking correctly (drift), weak actuation, two pantographs acting significantly differently … etc (5/11)
- blown ic chip (1/11)
- USB port broke off (1/11)

## More possible DFMA points
There are also some possible DFMA points to improve on, which will help us avoid issues with the hardware and fix them more easily

- LED to indicate the state of the firmware/ESP32
- easier way to mount and solder the motors (now it requires many steps and soldering positions that are hard to reach; also, replacing motors requires everything to be taken out)
- address the polarity of the motors (maybe use DIP switches or modify the motor to be foolproof)
- replacing/fixing the linkages requires the whole device to be taken out of the casing
- linkage bearing assembly: current design needs tweaking after assembly to act smoothly; it might have also led to mechanical issues with the haptics
- ribbon cables connecting to the handles have a pair of flipped wires due to different versions of the geared motors
- better way to zero the position of the handles; current process: move handles back to original position and then pressing reset button
- calibrate handle orientation: Patrick proposes adding gamified calibration routines that appear to be part of the (shooting) game. 


## Debugging Tools

0. More debuggable PCB design (in v5, each component can be swapped and tested)

1. **Firmware** to test PCB (testing both with and without battery) to check if

- firmware uploads
- esp32 turns on
- motor rotates
- encoder reads properly (maybe a jig to rotate motor exactly 1 revolution)
- motor rpm is in a reasonable region
- generate forcefield
- create obstacle
- move handle (“switch to” function)
- make one handle follow the other
- more?

2. Python script to test if the **USB communication** can
- receive heartbeat from Dualpanto (already done by Martin; found bugs and need to debug firmware)
- receive handle positions received successfully
- send message to move handles
- send message to place obstacles
- more?

3. A demo scene in **Unity** to test all the basic functions

4. Maybe a dualPanto emulator to check the packets that are sent from Unity for further debugging Unity.

P.s The ESP chip (ESP32-WROOM-32(M103QH2800PH3Q0)) we were using is now at the “not recommended for new design” stage, and not regularly stocked by Mouser/Digikey

P.p.s we may want to add an LED on the PCB to help with testing/debugging/validation. Moreover, might we need test jigs?

## Other non-device related things
The BPM team had audio queue up… is there a way to clear out the audio queue? Voice over should maybe be in German, so Silya Korn can understand?
