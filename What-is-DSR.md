# DSRemapper

## The name
DSRemapper is a cool way to call the program, but **DSRemapper** stands for **Device Switcher and Remapper**.

This name characterize the two main functionalities of this program, read a physical or emulated input device and remap it to a physical or emulated output one.

## What it does
DSRemapper was conceived with the intention to remap a physical game controller or joystick to a emulated one with the intention to use it for games which didn't recognice a old generic controller or to access advanced funtionalities on controllers like the DualShock 4 (the Sony PlayStation 4 controller).

After some test the program was scaling to a framework composed by plugins.
The framework work is to handle the devices and keep running the remapping function, but the device recognition or the remapping function are defined entirely by plugins.

This framework is capable from running a physical to emulated device remapping for games to any other thing that will require a constant update function to pass data from one "device" to another.
With "device" I mean anything that can be added with a plugin to the framework, for example, a TCP/IP port can be hosted by a plugin and the data recived by this translated to the internal framework structures.


