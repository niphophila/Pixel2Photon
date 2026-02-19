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
  - Unreal Engine 5.7. (process [here](https://www.unrealengine.com/en-US/download) if you've already got an epic games account/launcher/unreal engine, just make sure you have 5.7 installed)
  - Contents of project file(will be uploaded 18/02/2026) [here](https://drive.google.com/drive/folders/1ECqvWOB0zCVJSv94gVGdFEyaLC-d38DC?usp=sharing) downloaded . 


## Pre-Reading:

The main outcome of this workshop is sending information generated in touchdesinger to unreal engine via artnet in the same way you might send information to an actual light. This allows you to plan, test and design lighting systems before actually having access to the lights. We're simulating everything as accurately as possible, to avoid hiccups when its time to get physical.

I'm not going to go into the weird details about DMX and artnet and all that, [there is much written online](https://www.sweetwater.com/sweetcare/articles/understanding-dmx/) about the protocols and all that. Much of it won't be relevant to you because it assumes you want to program lights for Adele and I dont think you want to do that (its okay if you do). 

All you need to know is this:
- DMX (Digital Multiplex) is a protocol used to control hardware.
- Artnet is DMX over ethernet (this is good and cool)
- DMX consists of 512 individual channels of information, collectively are known as a 'universe'.
- Each channel can have a value of 0-255.
- Channels control different parameters of a device. What these parameters are, is determined by the device creator. Don't over think this, its important to keep it a bit abstract in the mind, because this protocol is DUMB, like you just shoot numbers at a device. it doesn’t know what they are, they're just numbers.
- Each channel is numbered and each device get to decide which channels it will 'listen' to. This is the device's address, which is the first channel which that device will use. How many channels the device will listen to after the initial address, is again up to the device/ their creator. Often you will set the address on the actual device (e.g address '1' will receive channel 1).

_  lil example_
 '''
   a hypothetical light thing can be either red, green or blue, theres a lil control circuit on there which says 'listen for 3 numbers (red 1,green 2,blue 3)' and 'my address is 30'. We send it three channels 30,31,32. If we send 30(255) 31(0) 32(0) it will be red!
   
  **the fuck around of dmx is making sure the information you send, lines up with the functions on the device**
  
   for instance, if we make an error and think that the things address is 31, we send 31(255) 32(0) 32(0) (remember its listening for (red(30, green(31) blue(32) it will be green, eiw :(

just keep this in mind and you'll be so fine! trust only the numbers,the meaning of the information we send is lost on the machine mind. 
'''
now that you know what the hell dmx even is , *we're going to use touchdesinger to send the the raw-ahh dmx, and we use virtual devices in unreal engine to make sure that dmx is doing things which we expect, just like it would IRL*

about the project file: This workshop project file is a modified version of the incred [DMX Sample Project created by Moment Factory  ](https://www.fab.com/listings/5ce617bc-b926-4db5-936b-a0733a5da72d). It is an incredible resource and shows the capability of unreal engine as a fully featured pre-vis environment. It's also very epic, and we don't quite need all the fancy things it provides. I have stripped it back to the really juicy bits. **They have done all the hard bits**.

The hardest thing they have done for us, is building the *fixture blueprints*. These blueprints are modular collections of 3D geometry, materials and  lights which have been pre-mapped to DMX inputs (most importantly, complex things, like moving lights with gobos etc.). You can create anything you can think of but its HARD. Don't worry too much about this capability for now, but know that its possible and feel grateful that it has been done for you (thanks!).

## Guide (i use windows, sorry if things are a bit different on mac)

 1. Extract the project file to a desired location. Make sure to keep the folder together. You should have a folder called Pixel2Photon_ExampleProj with two folders (config, content) and the UE project file inside.
 2. Open the Project file, it will load up. While its loading, check that it's opening in the right verison (5.7.3) otherwise you might have some weirdness. 
    
<img width="316" height="83" alt="image" src="https://github.com/user-attachments/assets/79304c98-7da9-4d32-aa4e-7a9b7f163a69" />

3. Unreal Editor will open, you'll see a mars looking place with some objects in the viewport (idk what its actually called) on the left, with the 'outliner' on the right showing you everything in the level. For now, dont go clicking on heaps of stuff. Here's how you get around:
   
<img width="2461" height="1392" alt="image" src="https://github.com/user-attachments/assets/62104f8d-89c8-4259-b2b8-460c83d1193f" />

<blockquote>
**The Viewport (Moving Around)**

The coolest way to move, because it feels like a video game.
  - Action	Control (Hold Right-Click)
  - Look Around	Move Mouse
  - Move Forward / Back	W / S
  - Strafe Left / Right	A / D
  - Move Up / Down	E / Q
  - Change Move Speed Scroll Mouse Wheel (while moving, this is how i usually get lost and zoom away)

  If you get lost select the 'home' in the Outliner (top right list) and press the F key to "Focus" (teleport) right to it.

**The "Classic" Navigation**

If you come from a 3D modeling background, you might prefer using the Alt key.

  - Alt + Left Click + Drag: Orbit around a selected object.
  - Alt + Right Click + Drag: Zoom in and out smoothly.
  - Alt + Middle Click + Drag: Pan (slide) the camera up, down, left, or right.

  **Manipulating Objects**

Once you’ve clicked on an object (like a light), you can use these hotkeys to move it. Look for the "Gizmo" (the colored arrows) to change.

  - W: Translate (Move)
  - E: Rotate
  - R: Scale (Resize)
  - G: Game View (Hides all the icons and gizmos so you can see what the game actually looks like).

**Key Panels**

If you ever close a window and can't find it, go to the Window menu at the top.

  - The Toolbar (Top): Where you "Play" the game or quickly add shapes/stuff.
  - The Outliner (Right): A text list of every single thing currently in your level.
  - Details Panel (Bottom Right): Where you change the settings of whatever you have selected (e.g., changing the color of a light).
  - Content Browser (Ctrl + Space): Your "File Explorer." This is where your models, sounds, and textures live.

</blockquote>

4. I've already populated this level with some lights to get us started; a moving head (MH_0) and an LED bar. Moving heads are literally robots and can swivel around as the name suggests. The LED bar is a strip of RGB LED's. In the outliner you can see both under the lights folder:
   
<img width="1157" height="777" alt="image" src="https://github.com/user-attachments/assets/73e8951c-899e-4a58-8c06-7d574c86485f" />

5. Click on the LED bar, and behold it's crazy blue lines (these show the extent of the light it casts, if they are ugly to you , hit G). In the details zone, you can see the light parameter. Scroll down to the DMX section, or in the little search box type 'dmx". You will see a line that says 'DMXlibrary', here is where we would select a library containing a dmx fixture map for our light. 'DMXLibv4' should be selected. Under this line you can see the 'fixture patch' field, here is where the corresponding dmx fixture map is selcted, 'MatrixStripRGB' should be selected.
>dmx fixture map refers to a virtual mapping of thedevice's fucntions to a corresponding channel, it will make sense
Double click on the dmx icon to open the DMX library.

 <img width="1267" height="1023" alt="image" src="https://github.com/user-attachments/assets/83373513-af8c-4ccc-89e6-724077fb8ddb" />

6. Now you will see the DMX library, this list shows all the pre-programmed dmx fixture maps available to you. You can see our Led Bar's fixture patch 'MatrixStripRGB in the list. Click on it, and under the modes list, select 60 Led Bar. On the right, you will see the channel configuration. 1.Red, 2.Green 3.Blue. You can also see that this mode will repeat this 60 times for each LED, resulting in a total of 180 channels!

<img width="1815" height="1066" alt="image" src="https://github.com/user-attachments/assets/620bb475-7c5e-428c-aeb3-36fadeedff35" />

7. This information is important, we need to send each LED 3 channels in the order red green blue, and there are 60 LED's. Click on the fixture patch tab. Here you will see this LED bar and the other light, shown graphically over what represents the whole DMX universe. You can tell which one is our LED Bar because its labelled, but also becuase it's taking up 180 channels. You can also see that it starts at channel 65. This is our fixture address. The zero's represent the DMX values currently being experienced by unreal engine. Dont worry about the other light for now.
    
<img width="1815" height="1066" alt="image" src="https://github.com/user-attachments/assets/558d90a6-3970-4689-aeb2-6aea8b3d6bf4" />

8. Okay time to light it up, open touchdesigner, save your project and call it something cool. hit tab and create a line POP. Under the points tab, set the X posiiton to 0.5 for both points, this will make the line vertical and in the 'middle'. Under divisions, set Divisions to 59 (for 60 points). These points will represent our LED's

<img width="478" height="414" alt="image" src="https://github.com/user-attachments/assets/1de4b399-14e8-47d1-9eec-116eae067bab" />

9. Next , create a lookup texture POP and connect the line. Under Output Attribute Scope, select Color. Create a null TOP and call it something profound like "led_tex", drag it onto the TOP reference of the lookup texture POP. Create a ramp TOP, set the Type to vertical and connect it to the null. nice

<img width="1313" height="926" alt="image" src="https://github.com/user-attachments/assets/f375641c-332d-4fa7-95ed-241509b88d05" /> 

10. Now, create a DMX fixture POP, name it something messed up like 'LED_bar" and connect the lookup texture to it. Set the universe to 1 , and the channel to 65 (cos remember?) Under the DMX profile tab name channel0 something wise like 'RGB' and then under Attribute select Color. Wow so easy and cool. Create a DMX out POP , the final piece of the puzz. 

<img width="1306" height="912" alt="Screenshot 2026-02-18 215803" src="https://github.com/user-attachments/assets/fc21ce01-441a-4672-a9dc-abc7d59e27e2" />

11. Lets inspect the DMX Out POP, this operator sends the dmx from touchdesigner to a device , in our case , the device is unreal engine on the same computer. So we want to send this to ourselves. Under the network tab, change the network address to be 127.0.0.1. This is an IP address that just means , me. If you wanted to send this to a real light you would enter the IP of the artnet node, or select a USB DMX device. Finally, lets check out what is going on under the hood. Click the first lil pink arrow of the DMXout POP, this will show us a table of everything being sent, and where its being sent to. switch the 'active' button on and zoom in on the table.

<img width="979" height="558" alt="Untitled" src="https://github.com/user-attachments/assets/aef10589-fc21-4fdf-a9ab-d1ed99865abb" />

<img width="1109" height="1045" alt="image" src="https://github.com/user-attachments/assets/83d08df9-8613-4e60-a467-99890e8c6502" />

12. Here we can see the first line is being sent to channel 65, universe 1, 127.0.0.1 and the value is 127 cool. second line, same but for channel 66, third for channel 68 but woah woah wtf why is the fouth line 255, and every fourth line after it also 255 , that aint right. and why are the first three values higher than the ones after if the gradient is a smooth change from 0-255? I'll tell you why, cos I SET YOU UP. Did you think this was a game!

<img width="259" height="194" alt="image" src="https://github.com/user-attachments/assets/41ef5870-588f-4e0e-a344-9ef42a3fd9b9" />

13. This fourth value is 255 because YOU sent it 255. Lets go back to Unreal engine to see whats going on over there. If everything is set-up correctly you should see a glowing stick. We can verify that unreal engine is getting dmx info by checking the 'Monitor DMX Input' box above the fixture patch. You should see some numbers, including 255 every 4th channel from channel 65! NICE but also wtf 

<img width="1293" height="716" alt="image" src="https://github.com/user-attachments/assets/3e8b86f7-ad44-45a6-8a4e-2ed6a742e5e7" />


<img width="217" height="668" alt="image" src="https://github.com/user-attachments/assets/54d0f846-055b-497b-b72d-de6c8468e9e9" /> 

14. cool but also bad because its not quite a gradient like we're trying to send it! the issue lies with our DMX fixture set up in Touchdesigner. The texture we are sending to the lookup POP has an alpha channel! We dont want to send that to the light because she has never even heard of alpha (only r,g,b). So go back to touchdesinger and select the DMX fixture POP you gave an awful name to. Under the DMX profile tab, change the attribute value  from just Color(RGBA)_, to Color(0) Color(1) Color(2) (RGB) and now check out the lil tabl, no more weird 255!

<img width="420" height="351" alt="image" src="https://github.com/user-attachments/assets/c7af24b1-fd35-4ffb-bbb6-9cc33a9bd67b" />

15. We still have that weird first pixel being 127. This is because our line starts at 1, and the pixel lookup has to choose between nothing or the texture at the border. Always make sure your geometry is well within those x1,y1 bounds! Put a transform pop in between the line and lookup. Set the scale to 0.9 and translate it 0.05 on the y axis. You could fix this 10000 ways but this works for now! While we're here lets animate the ramp, add an lfo CHOP, set it to type:ramp and frequency: 0.1 and reference it in the phase parameter of our ramp TOP. Feel free to plug whatever TOP you want into that null :)

Now go back to your light in unreal engine, it should be perfecto! aye nice! reap the dopamine! 

tbc....

16. Now that we've mastered a strip of LED's, we can apply these same techniques to any parameter of any other fixture profile. For instance, if you take a look at the other light in the project you'll see that it is 'listening' for 13 channels, 
- 01: Pan *you'l notice that the next channel is 3, this is because Pan is a 16 bit parameter meaning that it listens to the combination of two channels (1*2), this gives greater resolution in the value allowing the light to move with more precision!
- 02: Pan (again, cos 16bit)
- 03: Tilt 
- 04: Tilt *also 16bit*
- 05: Red
- 06: Green
- 07: Blue
- 08: Colour *preset colours*
- 09: Gobo *cool patterns*
- 10: Frost *its like blurry edges for gobo*
- 11: Zoom *makes the beam wider/smaller
- 12: Shutter *strobe/physical shutter*
- 13: Dimmer *brightness!*
 
<img width="1815" height="1066" alt="image" src="https://github.com/user-attachments/assets/bf613e99-ecd1-4fd9-aad4-19a109d6167a" />

These are classic parameters you'd find on a moving light, but its important to note that nothing is really standard. Each device will have its own fuctions, and channels and channel order etc. If you're trying to replicate a physical device you want to work with, you can re-map a fixture blueprint in unreal engine to match up (at least, more closley). You can find the fixture definitions for real-world devices in the manual, on device creator websites or the beautiful [GTDF Share database](https://gdtf-share.com/). A GTDF file is everything you need to program a light, there are even tools starting to appear to import these into unreal/TD! I'll try demonstrate this at the end! 

<img width="3021" height="2393" alt="image" src="https://github.com/user-attachments/assets/f5ffb61c-5037-4c4a-ad77-e66bd15566d1" />

So, lets create the control system for this in touchdesinger. Go back to TD and create a new point POP. This point represents out moving Create 8 attributes and name them:

- 01: Pan , set to 16bit
- 02: Tilt , set to 16bit
- 03: ColourWheel
- 04: GoboWheel 
- 05: Frost 
- 06: Zoom 
- 07: Shutter 
- 08: Dimmer

Copy the texture map pop and DMX fixture pop
