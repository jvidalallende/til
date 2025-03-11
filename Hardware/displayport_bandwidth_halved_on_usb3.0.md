# DisplayPort bandwidth is halved when USB3.0 is enabled

I faced a problem when trying to connect a laptop with DP 1.2 output to a 4K UHD monitor via USB-C cable.
My peers (which were using MacBooks with Thunderbolt 4) could use the monitor at native resolution.

However, although my laptop and cable worked fine most monitors on the same resolution, there was one monitor
where I could not get the output resolution to be higher than 2560x1440@60Hz.
I tried with my peer's cables (including ThunderBolt 4, even if my laptop could only use DP 1.2, just in case),
but nothing worked.

Then I came across [a reddit post][00] that explained a potential reason. I did not got to the very details,
but this section caught my attention:

_USB-C with DP Alt mode has 2 modes:_
- _allocate 2 of the 4 total high speed wire pairs to a "half" DP connection, the other 2 wire pairs
  remain available for USB3 (so up to 10G)_
- _allocate all 4 wire pairs for a full DP connection, same total bandwidth as a regular DP port with the same speed
  (which for DP are RBR, HBR1, HBR2, HBR3 currently). Only have USB2 available simultaneously_

So I got into the monitor settings, found out the USB speed one, and changed it from USB 3.0 to USB 2.0.
After that, I could get the monitor to display 3840x2160@60Hz.

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://www.reddit.com/r/UsbCHardware/comments/15unw6b/how_does_displayport_bandwidth_conflict_with_usb/?rdt=36592
