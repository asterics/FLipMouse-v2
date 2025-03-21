# FLipMouse V2


**Important:** This documentation refers to Version V2 of the FLipMouse, the new Version V3 is described here: [FLipmouse V3](https://github.com/asterics/FLipMouse).

The FLipMouse (a.k.a. Finger- and Lipmouse) is a replacement for a normal PC mouse / keyboard / joystick. 
Instead of moving the mouse device with your hand and clicking with your fingers, the FlipMouse can be controlled by applying very low forces to the mouthpiece (joystick) with your lips, fingers or other body parts.
The clicking functionality can be accomplished by sip- and puff-activities into the mouthpiece or via external switches.
All settings and functions of the FlipMouse can be tailored to specific user capabilites or needs. Multiple settings can be stored into the device and changed via desired user actions.
Additional features like built-in environmental control via infrared, optional bluetooth-add-on module for controlling smartphones/tablets or complete software-based control of all functions via serial command interface make the FlipMouse one of the most flexible alternative input devices available today.


![FLipmouse V2 mounted on Manfrotto Arm](/img/FLipmouse2.jpg)

The FlipMouse might be used as a full replacement of standard computer input devices and can also be used for accessing smartphones or tablets (via the standard HID support or accessibility features).
It can be useful for people with motor disablities, computer gamers, musicians or people who want a hands-free computer access for other purposes.

Our goal is to provide an affordable DIY-solution for everybody who wants to use a PC or smartphone with non-standard interaction methods.


# The DIY construction kit

The official FlipMouse DIY kit is available for purchase via https://hackerspaceshop.com/products/flipmouse-diy-kit. 
We provide a [Construction Manual](https://github.com/asterics/FLipMouse/blob/master/ConstructionKit/ConstructionManual.pdf) which shows how to assemble the kit. In case you want to buy the components from other sources, a full part list is available in folder [Hardware](https://github.com/asterics/FLipMouse/tree/master/Hardware).
There are different options for the enclosure: a laser-cut acrylic case (which is delivered in the DIY kit) and various 3d-printed variants. The desing files for enclosures can be found in folder [Hardware/case-design](https://github.com/asterics/FLipMouse/tree/master/Hardware/case-design).
The PCB designs (schematic and layout) have been made with EagleCAD/KiCad and are available in folder [Hardware/PCB-design](https://github.com/asterics/FLipMouse/tree/master/Hardware/PCB-design)

# Support us
If you want to support the development of FLipMouse you're very welcome to donate to the AsTeRICS Foundation:
<div><a title="Support AsTeRICS Foundation on betterplace.org!" target="_blank" href="https://www.betterplace.at/development-of-open-source-assistive-technologies"><img style="border:0px" alt="" src="https://betterplace-assets.betterplace.org/static-images/projects/donation-button-en.png" width="160" height="100"></a>
</div>

# Hardware and Features

The FLipMouse uses a [TeensyLC](https://www.pjrc.com/teensy/teensyLC.html) microcontroller (ARM CortexM0+ architecture) as main module. Movements of the mouthpiece are measured via FSRs (Force Sensing Resistors), which detect small forces applied to the mouthpiece / joystick.
The sip/puff actions are detected by a pressure sensor. Via two 3.5mm jack plugs, external momentary switches can be connected and desired actions can be assigned.
An IR-receiver module and a IR-LED allow recording and replay of arbitrary infrared remote control commands. Via an add-on module, bluetooth functionalty can be realized (for more information about the bluetooth add-on module please refer to the [FlipMouse Wiki](https://github.com/asterics/FLipMouse/wiki)


# Software (firmware and configuration manager)

The FLipMouse firmware is based on the Arduino/Teensyduino framework. The firmware implements a composite USB HID device (mouse, keyboard, joystick and a serial port in one device).
The mouse and keyboard device classes are used to transmit different keys or mouse actions to the host device. The serial port is used configure the FLipMouse (or even use it as a mouse simulator via AT commands).
Multiple configuration settings can be saved (stored in an EEPROM module) and changed via desired user actions.
For more information about (modifying) the FLipMouse firmware see https://github.com/asterics/FLipMouse/wiki/dev-firmware

## Configuration Manager

All settings of the FLipMouse can be changed via the [FlipMouse Configuration manager](https://flipmouse.asterics.eu)  
Using the configuration manager in the Chrome web browser, you can assign different actions to all hardware inputs of the FLipMouse (mouthpiece, sip and puff, external buttons,...).
The Configuration mananger can also be used to update the firmware of the FlipMouse and the optional Bluetooth module.

More Information can be found in the user manual: 
[user manual (english version)](https://github.com/asterics/FLipMouse/blob/master/Documentation/UserManual/Markdown/FLipMouseUserManual.md), 
[user manual (german version)](https://github.com/asterics/FLipMouse/blob/master/Documentation/UserManual/Markdown/FLipMouseAnwendungsanleitung.md).


## Building the firmware
In order to build the firmware following prerequisites and dependencies must be installed:
* the [Arduino IDE](https://www.arduino.cc/en/software) - use either IDE1 version 1.8.x or IDE2 verison 2.0.x
* the [Teensyduino](https://www.pjrc.com/teensy/td_download.html) add-on (must be compatible with the Arduino IDE version)
* the [SSD1306Ascii](https://github.com/greiman/SSD1306Ascii) library by Bill Greiman (can be installed using Arduino IDE's library manager)
* **important:** in the header file WireKinetis.h (Teensy Wire-library implemenation), *uncomment* the line `//#define WIRE_IMPLEMENT_WIRE1` - should be line number 50, see [here](https://github.com/PaulStoffregen/Wire/blob/2499ec67c2128629ee33697804f8650180293597/WireKinetis.h#L50). 
(This is needed to implement the Wire1 interface, which is disabled by default for the TeensyLC microcontroller in order to save memory.) 
  * If you are using a 1.8.x IDE version under Windows, the file is located inside a subfolder of the Arduino IDE installation, e.g.
`C:/Program Files (x86)/Arduino-1.8.19/hardware/teensy/avr/libraries/Wire/WireKinetis.h` 
  * If you are using a 2.0.x IDE version under Windows, the file is located inside a subfolder of Application Data, e.g.
`C:/Users/<YourName>/AppData/Local/Arduino15/packages/teensy/hardware/avr/1.58.0/libraries/Wire/WireKinetis.h`
* select the *board* 'Teensy LC' in the Arduino IDE tools menu
* select the *USB-type* 'Serial+Keyboard+Mouse+Joystick'  in the Arduino IDE tools menu
* select the correct *Port* after connecting the TeensyLC to your system
* compile and upload the firmware 


# Cleaning and Safety

**IMPORTANT:** If the mouthpiece is exposed to saliva, please clean/replace the mouthpiece (or its filter) on a regular basis, see [Safety Instructions](https://github.com/asterics/FLipMouse/blob/master/Documentation/Cleaning_instructions.pdf)

# Links to related projects

Most of the work for the FLipMouse has been accomplished at the UAS Technikum Wien in course of multiple research projects, see: ([AsTeRICS Foundation homepage](https://www.asterics-foundation.org)).

Maybe you want to have a look at our other AT-related Open Source projects:

* AsTeRICS: [AsTeRICS framework homepage](http://www.asterics.eu), [AsTeRICS framework GitHub](https://github.com/asterics/AsTeRICS): The AsTeRICS framework provides a much higher flexibility for building assistive solutions. 
The FLipMouse is also AsTeRICS compatible, so it is possible to use the raw input data for a different assistive solution.

* FABI: [FABI: Flexible Assistive Button Interface GitHub](https://github.com/asterics/FABI): The Flexible Assistive Button Interface (FABI) provides basically the same control methods (mouse, clicking, keyboard,...), but the input
is limited to simple buttons. Therefore, this interface is at a very low price (if you buy the Arduino Pro Micro from China, it can be under 5$).


# Troubleshooting / FAQ

### I cannot calibrate the FLipmouse, so that all 4 sensor values are in the same range

Usually this is caused by unequal forces on one (or more) of the 4 sensors. The reason is either:
* Displaced FSR sensor: please reposition the FSR to the center of the engraved circle
* Displaced rubber pad: please reposition the rubber pad to the center of the engraved circle
* Broken sensor: If it is possible, take a multimeter to measure the FSR value (should be down to 1-2kOhm with applied force)

### A thread of the enclosure screws (M3) is broken

There is no functional problem if one of the 4 screws are missing. If it is necessary to use this screw, the best solution is an extra attached screw nut.
Use a M3 screw nut (either plastic or metal) and glue it to the case. You need an extra screw, because the standard screws are to short for extra screw nuts.

### A thread of the sensor carrier (M4) is broken

The solution for this problem is the same as for the M3 screws. 
If you don't have longer M4 plastic screws, it is possible to remove a short piece of the spring. With a shorter spring, it is possible to drive the screw for a few extra mm.

### I dropped the FLipmouse and the case is broken

No problem, the acrylic glass can be glued again. Usually it is not as beautiful as before, but it works.
If you don't have the acrylic glass glue, you can use all types of glue which are able to glue acrylic glass.

### The mouse cursor moves without any force on the mouthpiece

This problem may have different causes. Please visit the wiki for further information: [Calibration](https://github.com/asterics/FLipMouse/wiki/calibration)



## Other problems?

Please visit the [wiki](https://github.com/asterics/FLipMouse/wiki).


![Front view of 3 FLipmice in different colors (black, pink and transparent orange)](/img/FLipmouse1.jpg)

