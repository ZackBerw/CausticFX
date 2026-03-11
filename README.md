# Black Box

Black Box is an open source DSP platform built on an Electrosmith Daisy Seed.

Originally derived from GuitarML’s Funbox project, Black Box is my contribution at getting the Max Msp Gen~ side of things running on the platform, along with providing a means to have swappable artwork for the pedal on top of making the project commercially available. As it only exists in the DIY sphere otherwise.

Black Box comes equipped with:
Stereo TRS input/output
6 potentiometers
3 threeway toggle switches
4 two way dipswitches
2 soft stomp switches 
2 LED indicator
⅛” TRS expression pedal input
⅛” TRS MIDI input
MIDI Clock synchronization
USB input port for Daisyseed
9V single barrel DC input

The origianl FunBox repository can be found here:
https://github.com/GuitarML/FunBox
_______________________________________________________________________________________________________________________________________________________________________________________________________

# Making my own Gen~ firmware

Here you can find the Max Msp Gen~ patch and json file that allows for you to get up and running with mapping your own patches to the Black Box hardware.

It’s also required to install the Oopsy Max package in the Max packages folder.

When it comes to getting the USART MIDI up and running it is important to note that the original Funbox PCB was designed around using pins 36/37, however the Oopsy package defaults the compiling process to pins 14/15. This is an easy one time fix that just requires changing the two numbers in the genlib_daisy.h file

After installing the Oopsy package navigate to the genlib_daisy.h file in the source folder. Open the file then scroll down to lines 508 and 509 and make this change:

config.pin_config.rx = {DSY_GPIOB, 15};
config.pin_config.tx = {DSY_GPIOB, 14};

You can find this portion of the code here and where it exists in the Oopsy package here:
https://github.com/electro-smith/oopsy/blob/5c9b1c83210cb1a9680087b32f5b7c6bdda71ac8/source/genlib_daisy.h#L495-L512

After you've made the change, save the H file and then you should be good to go!

_______________________________________________________________________________________________________________________________________________________________________________________________________

# Swapping Firmware

Swapping firmware on the Black Box is easy!
https://flash.daisy.audio/

Using Electrosmith’s web programmer, it’s as simple as holding down the right button followed by pressing the left button on the back of the daisy seed to put it into bootloader mode. From here you can upload whatever firmware speaks to you, as found on my GitHub repository or from someone else in the community.

If you’d like to write your own firmware in Max Msp Gen~ for instance, download the Black Box json file and Max Msp setup file also found on the GitHub repository. These files will give you everything you need in order to start connecting the hardware to software. That way when you flash the software using Oopsy everything will compile as desired.

To use Oopsy in Max just simply type in “Oopsy.petal” to create a bootloader object, then click the browse button. This is where you’ll load the supplied json file, which is required so the hardware knows how to communicate with the software. After loading that file ust press the big circle and wait 15 seconds for the firmware to be flashed. Now things should be up and running!

To install Oopsy for Max Msp head to the packages folder as found in the main Max Msp 9 folder. For my use case with Windows it’s: C:\Users\admin\Documents\Max 9\Packages

To download the Oopsy package head to this GitHub repository, then click the big Green button that says “Code”. From here it’ll open up a drop down menu giving you the option to “Download ZIP”. Unpack the zip and place the “oopsy” folder in the Max packages folder. For my use case with Windows it’s: C:\Users\admin\Documents\Max 9\Packages
https://github.com/electro-smith/oopsy

From here depending on if you’re a Windows or Mac user there are different procedures when it comes to getting things up and running. There are some great videos by Electrosmith themselves on the process. This is the video I followed for getting Oopsy to work, but there are more approaches depending on if you’d prefer to program in a different language. Be sure to do this process first before trying to swap firmware

How to Add Daisy Support to Max/MSP gen~
https://www.youtube.com/watch?v=HTXhd8sdxp4

How to Set Up Your C++ Development Environment (Daisy Tutorial)
https://www.youtube.com/watch?v=AbvaTdAyJWk

Note: you must use a micro USB B data transfer cable for this to work properly. A micro USB B cable that only charges will NOT be sufficient unfortunately. 
Chrome is also required for the web programmer to function properly.

