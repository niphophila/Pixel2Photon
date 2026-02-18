# Pixel2Photon
 ,-,-.
/ (_o \
\ o ) /
 `-'-'
Resources for Touch Collective Melbourne/ Altar Space, 2026 Pixel2Photon Workshop

*being actively updated before workshop*

16/02/2026: I'll put some resources here to make sure we can make the most of the hour workshop <3

Simulated Real-Time Lighting Control: TouchDesigner & Unreal Engine (now kith)

This project demonstrates the integration of TouchDesigner and Unreal Engine for virtual lighting simulation and remote control. It provides a basic framework for bridging a a touchdesigner programming and control interface with a high-fidelity virtual production environment in unreal engine to facilitate pre-visualization and system testing.

**Core Concepts**
  - System Integration: Establishing a real-time data bridge between TouchDesigner (control) and Unreal Engine (simulation).
  - Protocol understanding: Developing workflows for DMX and Art-Net addressing and signal routing. Make it make sense!
  - Pre-Visualization: Creating a virtual environment for testing scenography and lighting logic without physical hardware (other than a computer).

**Key Take-aways**
  - basis for a TD Control and programming interface for controlling hardware parameters via artnet(colour, movement, anything!)
  - Unreal Engine simulation project for real-time visual feedback of lighting designs. Program, address, and simulate lighting systems prior to physical deployment.
  - A feeling of internal power and limitless creative potential

**Requirements (pls bring and do)**

  Software: 
  please please please make sure you have downloaded and installed all software before the workshop (**files are big**!) to make sure you get the most juice out of lemon, esp the unreal engine install and first opening of project file (unreal engine will take a sec to ready the project!).
  - TouchDesigner (2025.32280) [link](https://derivative.ca/release/202532280/73761)
  - Unreal Engine 5.4. (process [here](https://www.unrealengine.com/en-US/download) if you've already got an epic games account/launcher/unreal engine, just make sure you have 5.4 installed)
  - Contents of project file(will be uploaded 18/02/2026) [here](https://drive.google.com/drive/folders/1ECqvWOB0zCVJSv94gVGdFEyaLC-d38DC?usp=sharing) downloaded . 


# Pre-Reading:

The main outcome of this workshop is sending information generated in touchdesinger to unreal engine via artnet in the same way you might send information to an actual light. This allows you to plan, test and design lighting systems before actually having access to the lights. We're simulating everything as accurately as possible, to avoid hiccups when its time to get physical.

I'm not going to go into the weird details about DMX and artnet and all that, [there is much written online](https://www.sweetwater.com/sweetcare/articles/understanding-dmx/) about the protocols and all that. Much of it won't be relevant to you because it assumes you want to program lights for Adele and I dont think you want to do that (its okay if you do).

All you need to know is this:
- DMX (Digital Multiplex) is a protocol used to control hardware.
- Artnet is DMX over ethernet (this is good and cool)
- DMX consists of 512 individual channels of information, collectively are known as a 'universe'.
- Each channel can have a value of 0-255.
- Channels control different parameters of a device. What these parameters are, is determined by the device creator. Don't over think this, its important to keep it a bit abstract in the mind, because this protocol is DUMB, like you just shoot numbers at a device. it doesn’t know what they are, they're just numbers.
- Each channel is numbered and each device get to decide which channels it will 'listen' to. This is the device's address, which is the first channel which that device will use. How many channels the device will listen to after the initial address, is again up to the device/ their creator. Often you will set the address on the actual device (e.g address '1' will receive channel 1).

  lil example
   a hypothetical light thing can be either red, green or blue, theres a lil control circuit on there which says 'listen for 3 numbers (1,2,3)' and 'my address is 30'. We send it three channels 30,31,32. If we send 30(255) 31(0) 32(0) it will be red!
  **the fuck around of dmx is making sure the information you send lines up with the functions on the device**
   for instance, if we make an error and think that the things address is 31, we send 31(255) 32(0) 32(0) (remember its listening for (red(30, green(31) blue(32) it will be green, eiw :(

just keep this in mind and you'll be so fine! trust only the numbers,the meaning of the information we send is lost on the machine mind. 

now that you know what the hell dmx even is , *we're going to use touchdesinger to send the the raw-ahh dmx, and we use virtual devices in unreal engine to make sure that dmx is doing things which we expect, just like it would IRL*

  
# Instrucitons:


 

    
...
